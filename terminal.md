---
layout: null
hide-in-nav: true
permalink: /terminal/
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>terminal</title>
    <style>
        /* init */
        html, body { margin: 0 !important; padding: 0 !important; background-color: black !important; color: #FFFFFF !important; width: 100% !important; height: 100vh !important; overflow: hidden !important; font-family: 'Courier New', Courier, monospace; box-sizing: border-box; }
        /* layout */
        .terminal-wrapper { width: 100%; height: 100%; padding: 20px; box-sizing: border-box; overflow-y: auto; display: flex; flex-direction: column; }
        .output-history { white-space: pre-wrap; line-height: 1.5; font-size: 14px; }
        .input-line { display: flex; align-items: center; margin-top: 5px; font-size: 14px; }
        .prompt { margin-right: 10px; user-select: none; }
        /* cmd input */
        .cmd-field { background: transparent; border: none; color: #FFFFFF; font-family: inherit; font-size: inherit; outline: none; flex: 1; padding: 0; }
        .terminal-wrapper::-webkit-scrollbar { width: 0px; background: transparent; }
    </style>
</head>
<body>
    <div class="terminal-wrapper" id="terminal-screen">
        <div class="output-history" id="history-box">CORE ARCHITECTURE [VERSION 1.0.16]
(C) 2026 MICHU. ALL RIGHTS RESERVED.

Welcome. 

Type 'help' to view available commands.

</div>
        <div class="input-line">
            <span class="prompt" id="terminal-prompt">visitor@terminal.html ~ %</span>
            <input type="text" class="cmd-field" id="user-input" autofocus autocomplete="off" spellcheck="false">
        </div>
    </div>
    <script>
        const inputField = document.getElementById('user-input');
        const historyBox = document.getElementById('history-box');
        const screenBox = document.getElementById('terminal-screen');
        const promptLabel = document.getElementById('terminal-prompt');        
        const helpText = `Available commands:\n  cd [dir]    Dynamic routing jump to any valid page suffix / permalink\n  ls          List memory nodes or structural entities in current sector\n  cat [file]  Read stream payload from a specific target node\n  clear       Clear the terminal screen\n  help        Display this information map`;
        let currentContext = { isSandboxActive: false, activeAgent: 'visitor', currentPath: '/' };
        let sandboxFS = {};
        fetch('/arg_gateway.json', { cache: 'no-store' }).then(res => res.json()).then(data => { sandboxFS = data || {}; }).catch(err => { sandboxFS = {}; printLine('Warning: Remote blueprint gateway mapping offline.'); });
        document.addEventListener('click', () => { inputField.focus(); });
        inputField.addEventListener('keydown', function(event) {
            if (event.key === 'Enter') {
                event.preventDefault();
                const rawInput = this.value;
                const cleanInput = rawInput.trim();                  
                printLine(`${currentContext.activeAgent}@terminal.html ${currentContext.currentPath === '/' ? '~' : currentContext.currentPath} % ${rawInput}`);                
                if (cleanInput.length > 0) { executeCommand(cleanInput); }
                this.value = '';
                screenBox.scrollTop = screenBox.scrollHeight;
            }
        });
        function printLine(text) {
            const secureText = text.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
            historyBox.innerHTML += secureText + '\n';
            screenBox.scrollTop = screenBox.scrollHeight;
        }
        function syncPromptUI(agent, path) { currentContext.activeAgent = agent; currentContext.currentPath = path; promptLabel.textContent = `${agent}@terminal.html ${path === '/' ? '~' : path} %`; }
        function executeCommand(cmdStr) {
            const trimmedStr = cmdStr.trim();
            const firstSpace = trimmedStr.indexOf(' ');
            const cmd = (firstSpace === -1 ? trimmedStr : trimmedStr.substring(0, firstSpace)).toLowerCase();
            const arg = (firstSpace === -1 ? "" : trimmedStr.substring(firstSpace).trim());
            switch (cmd) {
                case 'help':
                    printLine(helpText);
                    break;
                case 'clear':
                    historyBox.textContent = '';
                    break;
                case 'ls':
                    if (currentContext.isSandboxActive && sandboxFS && sandboxFS[currentContext.currentPath]) {
                        const roleData = sandboxFS[currentContext.currentPath][currentContext.activeAgent];
                        if (roleData && roleData.files) { printLine(roleData.files.join('    ')); }
                        else { printLine(`ls: current agent matrix directory is empty.`); }
                    } else {
                        inputField.disabled = true;
                        const targets = ['index.html', 'about.html', 'archive.html', 'gallery.html', 'search.json', 'feed.xml', '404.html'];
                        let discovered = [];
                        let probes = targets.map(t => fetch('/' + t, { method: 'HEAD' }).then(res => { if (res.ok) discovered.push(t); }));
                        Promise.all(probes).then(() => {
                            inputField.disabled = false; inputField.focus();
                            printLine(discovered.length > 0 ? discovered.join('    ') : 'ls: no structural public nodes exposed in this segment.');
                        });
                    }
                    break;
                case 'cat':
                    if (!arg) { printLine('usage: cat [file_name]'); break; }
                    if (currentContext.isSandboxActive && sandboxFS && sandboxFS[currentContext.currentPath]) {
                        const roleData = sandboxFS[currentContext.currentPath][currentContext.activeAgent];
                        if (roleData && roleData.content && roleData.content[arg]) { printLine(roleData.content[arg]); }
                        else { printLine(`cat: ${arg}: No such node stream in your agent inventory profile`); }
                    } else {
                        let targetFile = arg;
                        if (!targetFile.startsWith('/')) targetFile = '/' + targetFile;
                        inputField.disabled = true;
                        fetch(targetFile).then(res => {
                            if (!res.ok) throw new Error();
                            return res.text();
                        }).then(text => {
                            inputField.disabled = false; inputField.focus();
                            printLine(text.slice(0, 1500) + (text.length > 1500 ? '\n... [TRUNCATED SYSTEM STREAM PAYLOAD]' : ''));
                        }).catch(() => {
                            inputField.disabled = false; inputField.focus();
                            printLine(`cat: ${arg}: Standard physical file stream resource not found`);
                        });
                    }
                    break;
                case 'cd':
                    if (!arg || arg === '~' || arg === '/') {
                        currentContext.isSandboxActive = false;
                        syncPromptUI('visitor', '/');
                        printLine('Returned to baseline root directory: /');
                    } else {
                        let target = arg;
                        if (!target.startsWith('/')) target = '/' + target;
                        if (!target.endsWith('/')) target = target + '/';
                        if (sandboxFS && sandboxFS[target]) {
                            currentContext.isSandboxActive = true;                           
                            const availableAgents = Object.keys(sandboxFS[target]);
                            const rollingName = availableAgents[Math.floor(Math.random() * availableAgents.length)];                           
                            printLine(`Warning: Shifted tracking path to internal sandbox loop...\nIdentity matrix corrupted. Quantum handshake shift completed.`);                            
                            syncPromptUI(rollingName, target);
                            break;
                        }
                        /* checkpoint fallback: absolute static safety redirect block */
                        if (target === '/sandbox/') {
                            currentContext.isSandboxActive = true;
                            const staticAgents = ['M.E.M.O.', 'Lyin_', 'invidia'];
                            const rollingName = staticAgents[Math.floor(Math.random() * staticAgents.length)];
                            printLine(`Warning: Sandbox dynamic override routing active.\nIdentity matrix corrupted. Quantum handshake shift completed.`);
                            syncPromptUI(rollingName, target);
                            break;
                        }
                        printLine(`Probing destination node: ${target} ...`);                       
                        inputField.disabled = true;
                        fetch(target, { method: 'HEAD' })
                        .then((response) => {
                            inputField.disabled = false;
                            inputField.focus();
                            if (response.ok) {
                                printLine(`Routing handshake established. Syncing...`);
                                setTimeout(() => { window.location.href = target; }, 400);
                            } else { printLine(`cd: ${arg}: Suffix destination or permalink not found`); }
                        })
                        .catch((error) => {
                            inputField.disabled = false;
                            inputField.focus();
                            printLine(`cd: connection handshake timeout on route: ${arg}`);
                        });
                    }
                    break;
                default:
                    printLine(`zsh: command not found: ${cmd}. Type 'help' for map.`);
                    break;
            }
        }
    </script>
</body>
</html>

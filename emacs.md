# Emacs Perspective Mode Command Reference

## Workspace Switching & Navigation
*   `<prefix> s` (`persp-switch`)
    *   Switches to a perspective or creates a new one if the name does not exist.
*   `<prefix> \`` (`persp-switch-by-number`)
    *   Switches to a perspective using its index number (1, 2, 3, etc.).
*   `<prefix> n` or `<prefix> <right>` (`persp-next`)
    *   Cycles forward to the next sequential perspective.
*   `<prefix> p` or `<prefix> <left>` (`persp-prev`)
    *   Cycles backward to the previous perspective.

## Buffer Management
*   `<prefix> b` (`persp-switch-to-buffer`)
    *   Works like standard `switch-to-buffer`, but lets you switch to any buffer across all perspectives, changing the active perspective automatically if necessary.
*   `<prefix> a` (`persp-add-buffer`)
    *   Adds an existing open buffer into your current active perspective.
*   `<prefix> A` (`persp-set-buffer`)
    *   Adds a buffer to the current perspective while simultaneously removing it from all other active perspectives.
*   `<prefix> k` (`persp-remove-buffer`)
    *   Removes a specified buffer from the current perspective without killing the buffer itself.
*   `<prefix> g` (`persp-add-buffer-to-frame-global`)
    *   Adds a buffer to a frame-specific, globally shared perspective.

## Perspective Manipulation
*   `<prefix> c` (`persp-kill`)
    *   Closes and completely deletes a perspective.
*   `<prefix> r` (`persp-rename`)
    *   Changes the name of the current active perspective.
*   `<prefix> i` (`persp-import`)
    *   Imports a perspective and its workspace context from another Emacs frame.
*   `<prefix> m` (`persp-merge`)
    *   Temporarily merges all buffers from a targeted perspective into your current one.
*   `<prefix> u` (`persp-unmerge`)
    *   Reverses a previous merge operation, separating the merged buffers back into their own perspective.

## State Persistence
*   `<prefix> C-s` (`persp-state-save`)
    *   Saves the layout and states of all active perspectives across all frames into a persistent file.
*   `<prefix> C-l` (`persp-state-load`)
    *   Loads previously saved layouts and perspectives back into your current session from a file.

# Emacs Dape setup(Attach mode)

;; =========================================================================
;; COMPLETE EMACS + TRAMP + DOCKER + DAPE + DEBUGPY SPECIFICATION
;; =========================================================================

(use-package dape
  :ensure t
  :config
  ;; 1. WINDOW LAYOUT & UI CONFIGURATION
  ;; Opens the debugger panels on the right side of the screen.
  ;; This gives you an IDE-like view of variables, breakpoints, and the call stack.
  (setq dape-buffer-window-arrangement 'right)

  ;; 2. REPL MANAGEMENT
  ;; Directs execution logs and console outputs from the debugger's evaluation 
  ;; loop into a dedicated Emacs buffer instead of hijacking your main frame.
  (add-hook 'dape-compile-compile-hooks 'dape-repl-use-buffer)

  ;; 3. DOCKER TRAMP PROFILE CONFIGURATION
  ;; Defines a unified debugging configuration customized for your container.
  (add-to-list 'dape-configs
               `(debugpy-remote-tramp-docker
                 ;; Activates this profile strictly when inside Python source buffers
                 modes (python-mode python-ts-mode)
                 
                 ;; Connects to localhost because the SSH tunnel maps the 
                 ;; remote container's network directly to your host loopback.
                 host "localhost"
                 port 5678
                 
                 ;; Explicitly instructs Dape to use the Python engine backend
                 :type "python"
                 
                 ;; "attach" decouples execution from editing. TRAMP will not freeze 
                 ;; because Emacs does not attempt to handle target process signals.
                 :request "attach"
                 
                 ;; PATH MAPPING (Crucial translation layer)
                 ;; :remoteRoot -> The exact target WORKDIR inside your Dockerfile.
                 ;; :localRoot  -> Evaluates 'default-directory' dynamically at runtime. 
                 ;;                 Because you are in a TRAMP file buffer, it cleanly grabs
                 ;;                 the remote identifier (e.g., "/ssh:dev@remote:/workspace/").
                 :pathMappings [(:remoteRoot "/workspace" :localRoot default-directory)]
                 ))
  
  :bind
  ;; 4. GLOBAL KEYBINDINGS FOR STEPPING & VARIABLE INSPECTION
  (("C-c d d" . dape)                  ;; Launch debugger UI / Select profile
   ("C-c d b" . dape-breakpoint-toggle) ;; Toggle a visual breakpoint on the current line
   ("C-c d n" . dape-next)              ;; Step Over (Execute next line of code)
   ("C-c d s" . dape-step-in)           ;; Step Into (Descend into current function)
   ("C-c d o" . dape-step-out)          ;; Step Out (Escape current function scope)
   ("C-c d c" . dape-continue)          ;; Continue execution to the next breakpoint
   ("C-c d r" . dape-repl)              ;; Jump context directly to the active REPL prompt
   ("C-c d w" . dape-watch-dwim)        ;; Track current variable in persistent sidebar
   ("C-c d q" . dape-quit)))            ;; Terminate / Disconnect debugger session

;; =========================================================================
;; OPERATIONAL RUNNING INSTRUCTIONS (COPY & PASTE FOR YOUR TERMINALS)
;; =========================================================================
;;
;; STEP 1 [Local Machine Terminal]: Open the Network Bridge / SSH Tunnel
;; ssh -L 5678:localhost:5678 dev@your-remote-server-ip
;;
;; STEP 2 [Remote Container Shell]: Launch your App with Debugpy
;; python -m debugpy --listen 0.0.0.0:5678 --wait-for-client main.py
;;
;; STEP 3 [Emacs]: Open file via TRAMP, set breakpoint (C-c d b), 
;; run M-x dape (C-c d d) and choose 'debugpy-remote-tramp-docker'.
;;
;; STEP 4 [Variable Printing]: 
;; Look at the automatically updated '*dape-info Variables*' sidebar window,
;; or switch to the REPL (C-c d r) and type raw Python expressions directly.
;; =========================================================================


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

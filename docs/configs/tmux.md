### Old config

```
# --------#
# General #
# --------#

# Default shell
set -g default-shell $SHELL

# Mouse
set -g mouse on

# History
set -g history-limit 102400

# Set windows and page index to base 1
set -g base-index 1
setw -g pane-base-index 1

# Re-number windows when creating/closing new windows
set -g renumber-windows on

# Use emacs key bindings in status line
set-option -g status-keys emacs

# Use vim key bindings in copy mode
setw -g mode-keys vi

# Fix ESC delay in vim
set -g escape-time 10

# ------------#
# Keybindings #
# ------------#

# Set prefix to C-a
unbind C-b
set -g prefix C-a

# Copy-mode
unbind-key -T copy-mode-vi v
bind-key -T copy-mode-vi v send-keys -X begin-selection
bind-key -T copy-mode-vi 'C-v' send-keys -X rectangle-toggle
bind-key -T copy-mode-vi y send-keys -X copy-pipe-and-cancel "pbcopy"
bind-key -T copy-mode-vi MouseDragEnd1Pane send-keys -X copy-pipe-and-cancel "pbcopy"

# Send command on double press
bind C-a send-prefix
bind C-l send-keys 'C-l'

# Reload tmux.conf on prefix r
bind r source-file ~/.tmux.conf \; display "Config reloaded!"

# Split panes and remember current path
bind '\' split-window -h -c '#{pane_current_path}'
bind - split-window -v -c '#{pane_current_path}'

# Remember current path when creating new windows
bind c new-window -c '#{pane_current_path}'

# Break pane into new window and keep focus on the current window
bind b break-pane -d

# Smart pane switching with awareness of Vim splits.
is_vim="ps -o state= -o comm= -t '#{pane_tty}' \
    | grep -iqE '^[^TXZ ]+ +(\\S+\\/)?g?(view|n?vim?x?)(diff)?$'"
bind-key -n C-h if-shell "$is_vim" "send-keys C-h"  "select-pane -L"
bind-key -n C-j if-shell "$is_vim" "send-keys C-j"  "select-pane -D"
bind-key -n C-k if-shell "$is_vim" "send-keys C-k"  "select-pane -U"
bind-key -n C-l if-shell "$is_vim" "send-keys C-l"  "select-pane -R"
bind-key -n 'C-\' if-shell "$is_vim" "send-keys 'C-\'" "select-pane -l"
bind-key -T copy-mode-vi C-h select-pane -L
bind-key -T copy-mode-vi C-j select-pane -D
bind-key -T copy-mode-vi C-k select-pane -U
bind-key -T copy-mode-vi C-l select-pane -R
bind-key -T copy-mode-vi 'C-\' select-pane -l

# -----------#
# Status bar #
# -----------#
# Status line colours
set -g status-bg black
set -g status-fg white

# window list colours
set -g window-status-style bg=default,fg=white
set -g window-status-current-style bg=red,fg=white,bright

# Status bar left
set -g status-left-length 20
set -g status-left ""
set -g status-interval 10
set -g status-justify right

# status bar right
set -g status-right "[#S] #[fg=blue,bold]#(cat /proc/loadavg | awk '{print $1,$2,$3}')"

# activity alerts
setw -g monitor-activity on
set -g visual-activity on


# # Status Bar
# set-option -g status-interval 1
# set-option -g status-left ''
# set-option -g status-right '%l:%M%p'
# set-window-option -g window-status-current-style fg=blue
# set-option -g status-style fg=default

# set-option -g status-position top
# set-option -g status-justify left
# set-option -g status-left '#[bg=colour72] #[bg=colour237] #[bg=colour236] #[bg=colour235]#[fg=colour185] #S #[bg=colour236] '
# set-option -g status-left-length 16
# set-option -g status-bg colour237
# set-option -g status-right '#[bg=colour236] #[bg=colour235]#[fg=colour185] %a %R #[bg=colour236]#[fg=colour3] #[bg=colour237] #[bg=colour72] #[]'
# set-option -g status-interval 60

# set-option -g pane-active-border-style fg=colour246
# set-option -g pane-border-style fg=colour238

# set-window-option -g window-status-format '#[bg=colour238]#[fg=colour107] #I #[bg=colour239]#[fg=colour110] #[bg=colour240]#W#[bg=colour239]#[fg=colour195]#F#[bg=colour238] '
# set-window-option -g window-status-current-format '#[bg=colour236]#[fg=colour215] #I #[bg=colour235]#[fg=blue] #[bg=colour234]#W#[bg=colour235]#[fg=colour195]#F#[bg=colour236] '
```


### New config
```
set -g default-terminal "screen-256color"

set -g prefix C-a
unbind C-b
bind-key C-a send-prefix

# Split panes and remember current path
bind '\' split-window -h -c '#{pane_current_path}'
bind - split-window -v -c '#{pane_current_path}'

# Remember current path when creating new windows
bind c new-window -c '#{pane_current_path}'

unbind r
bind r source-file ~/.tmux.conf

bind -r j resize-pane -D 5
bind -r k resize-pane -U 5
bind -r l resize-pane -R 5
bind -r h resize-pane -L 5

bind -r m resize-pane -Z

set -g mouse on

set-window-option -g mode-keys vi

bind-key -T copy-mode-vi 'v' send -X begin-selection # start selecting text with "v"
bind-key -T copy-mode-vi 'y' send -X copy-selection # copy text with "y"

unbind -T copy-mode-vi MouseDragEnd1Pane # don't exit copy mode when dragging with mouse

# tpm plugin
set -g @plugin 'tmux-plugins/tpm'

# list of tmux plugins
set -g @plugin 'christoomey/vim-tmux-navigator'
set -g @plugin 'jimeh/tmux-themepack'
set -g @plugin 'tmux-plugins/tmux-resurrect' # persist tmux sessions after computer restart
set -g @plugin 'tmux-plugins/tmux-continuum' # automatically saves sessions for you every 15 minutes

set -g @themepack 'powerline/default/cyan'

set -g @resurrect-capture-pane-contents 'on'
set -g @continuum-restore 'on'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

### Running the config
To install the tpm plugins, run run `CTRL + a`, then `SHIFT + i`

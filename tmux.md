Tmux Configuration
=

Overview
-

I love TMUX! -- Let me repeat, I love TMUX! Installing with my custom bash aliases for initialization combined with custom scrolling, its the most wonderful thing to happen to my terminal.

Here's What I Did to enable scrolling with my trackpad:

	1.) Install SIMBL -- This is a system level program that forwards mouse events to the proper programs
		(http://www.culater.net/software/SIMBL/SIMBL.php)

	2.) Install SIMBL Plugin for Terminal.app
		(http://code.google.com/p/simbl/wiki/SIMBLPlugins)

	3.) Set the following tmux.conf settings:

		# set window
		set-option -g mouse-select-window on

		# should allow us to scroll but not working
		set -g mode-mouse on

		# Allow mouse to select which pane to use
		setw -g mouse-select-pane on

https://mutelight.org/practical-tmux
		



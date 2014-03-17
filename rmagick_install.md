Installing ImageMagick / Rmagick with RVM Mountain Lion
=

Overview
-

Today, I was trying to install rmagick to do some quick resizing of images in a ruby script. I'm running my own gemset within rvm. When I ran gem install rmagick, I got all kinds of errors saying that headers were not found for imagemagick on my machine. Here's what I did to solve the problem...


Installing RMagick on Mountain Lion
-

Step 1 : clean system / prepare

	//make sure you have homebrew installed
	//be sure to uninstall old imagemagick if included:
	brew uninstall imagemagick

Step 2: install imagemagick without openmp support.

	For some reason unless you exclude the openmp library in your installation, you will have problems using rmagick

	brew install imagemagick --disable-openmp

Step 3: symlink some required system libraries in homebrew

	cd into your cellar and then the imagemagic installation's lib folder.

	mine is here: /usr/local/Cellar/imagemagick/6.8.0-10/lib

	Then you will want to symlink some libraries to help the installation complete

	ln -s libMagick++-Q16.7.dylib   libMagick++.dylib
	ln -s libMagickCore-Q16.7.dylib libMagickCore.dylib
	ln -s libMagickWand-Q16.7.dylib libMagickWand.dylib

Step 4: run gem install rmagick again.

	You shouldn't have any problems. For me, I got errors that said no-definition for like 100 or so different functions. The previous steps helped me solve these problems, and everything seems to be running great now!






Custom Mac GCC
=

Mac Mountain Lion and older versions are pretty set on you using XCode's included GCC version, but often times you may want to include a new version. In my case, the Homebrew package manager's version of apple-gcc-4.2 wasn't cutting it and I was eager to test the latest and greatest from gcc. It's a relatively simple installation but can cause havoc on the rest of your system. 

What I did was install it into usr/local/gcc and made sure that this bin was not on my path. Since I'm only installing gcc for certain applications and mostly to play around with the new features of C++ 11, I was okay with just creating an alias and directing to that instead.

First steps:

1.) Make sure homebrew is installed and updated. Make sure you have also installed wget, tar and bzip.

2.) Go into your /usr/local/src directory (this is where most unix systems should load src code. Personally, I keep many applications configured here so when I need to re-install I can just run make && make install quickly to fix anything I mess up.) 

3.) run wget http://www.netgull.com/gcc/snapshots/LATEST-4.8/gcc-4.8-20130113.tar.bz2
  
  This will grab the bzip2 package and will download it into the src directory.

4.) run bzip2 -d file_name_that_was_downloaded 
  
  This will give you a tar file that you can decompress

5.) decompress the tar file by running tar -xvf file_name 

  This will now give you the source code in its own directory.

6.) cd into the directory and then run ./configure. You will probably get some errors that say its missing some libraries. I fixed this by running `brew install gmp mpfr mpc libmpc` 

  If this doesn't fix this try looking in the error logs in the same directory or look through the message and try to install those packages.

  This worked fairly well on mac mountain lion.


7.) Now that you have the source code configured, you should be ready to run make (this will take a long time). I personally recommend running this in a tmux-session or screen-session so you can continue to work on your machine.

8.) run `make DESTDIR=/usr/local/gcc` install 

  This will now install the binaries and application into your /usr/local/gcc folder

  While keeping software in this folder can throw some trouble homebrew's way, (you will notice when running brew doctor) I prefer this because none of those errors have ever caused me install problems with other apps and this allows you to alias or put these in the path as needed, and export your dotfiles to other unix-systems where this is the recommended install place for user-compiled software. (Just my recommendation though)

9.) alias the gcc. You can edit your ~/.bashrc or ~/.bash_profile. For mac users who don't know what I'm talking about just copy this one-liner in:

  echo "alias gcc-4.8='/usr/local/gcc/bin/gcc'" >> ~/.bash_profile && source ~/.bash_profile

You should be good to go, personally I don't recommend adding this to your path on mac as it will mess up many installations that are mac based and want either the xcode gcc or the clang version.


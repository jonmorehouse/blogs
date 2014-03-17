Getting Json Up and Running with C++
=

Overview
=

I'm starting an OpenGL program and was hoping to have most variables / points loaded in via JSON upon program initialization so that I don't have to recompile between visual changes.

Getting a Library
=

I'm using the library Jansson ![Jansson](https://github.com/akheron/jansson)

I personally symlinked it to /usr/local/jansson after installing in a different direction. (I forked this project and am planning to add some other functionality later in the future)

	ln -s /usr/local/jansson ~/Documents/general_development/public_code/jansson

Basic Compiling
=

pkg-config -- this is a .pc file

	running `pkg-config --libs --cflags jansson`

	Will give you the proper -I include directives for your machine

	output = -I/usr/local/include  -L/usr/local/lib -ljansson  

Can run this in your g++ stream for easy compilation! Otherwise use these values manually in a make file


Google Solution
=

Googlemock / GoogleTest work best when you compile them locally as dylibs for your code base. Thus, I just used the google directory as a variable and went from there


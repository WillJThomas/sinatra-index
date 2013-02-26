# Sinatra Indices

The problem: you want the path `/` to give the contents of `public/index.html` and `/foo`, to go to `public/foo/index.html`.

The solution:

    require 'rubygems'
	require 'sinatra-index'
    
    class MyApp < Sinatra::Base
      register Sinatra::Index
      use_static_index 'index.html'
	  
	  ... Sinatra routes ...
	end

The route will only be overridden if it cannot be routed using your defined Sinatra configuration e.g. if you have a block like this:

use_static_index 'index.html'

get '/defined' do
    'Hello world!'
end

the path '/defined' will respond with 'Hello world!'; it will not try and load /defined/index.html file.
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

NOTE: static files are given precedence over dynamic routes in sinatra - this library confirms to this e.g. if you have a block like this:

use_static_index 'index.html'

get '/defined' do
    'Hello world!'
end

if a /defined/index.html file exists, this will be the response - not 'Hello world!'.
If you wish for your dynamic route to work then move or delete the /defined/index.html file
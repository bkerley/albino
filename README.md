# Albino: a ruby wrapper for pygmentize

This project is a hack of an extraction from GitHub.

The issue I faced is that Ryan Tomayko's 
[rocco](https://github.com/rtomayko/rocco) literate programming tool
depends on this. That's cool, but albino used to depend on posix-spawn,
which depends on a C library, which won't work in JRuby.

This fork removes posix-spawn, instead using popen, which works just
fine in JRuby on Mac OS X. As a casualty, the API for Albino#execute
has changed, for which I am <s>deeply sorry</s> unapologetic.

## Installation

    sudo easy_install pygments
    gem install albino

## Usage

### Simple

    require 'albino'
    puts Albino.colorize('puts "Hello World"', :ruby)

### Advanced

    require 'albino'
    @syntaxer = Albino.new(File.new('albino.rb'), :ruby, :bbcode)
    puts @syntaxer.colorize

### Multi

    require 'albino/multi'
    ruby, python = Albino::Multi.colorize([ [:ruby,'1+2'], [:python,'1-2'] ])


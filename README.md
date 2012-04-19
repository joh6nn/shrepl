shrepl(1) -- sometimes you need a repl
====================================

`shrepl` is a POSIX-shell--compliant clone of Chris Wanstrath's
`repl`. It is an interactive program which tenderly wraps another,
non-interactive program.

For example:

    $ shrepl redis-cli -p 6665
    >> set name chris
    OK
    >> get name
    chris
    >> info
    redis_version:1.000
    uptime_in_seconds:182991
    uptime_in_days:2
    .. etc ..


Or:

    $ shrepl gem
    >> --version
    1.3.5
    >> search yajl

    *** LOCAL GEMS ***

    yajl-ruby (0.6.7)
    >> search yajl -r

    *** REMOTE GEMS ***

    brianmario-yajl-ruby (0.6.3)
    filipegiusti-yajl-ruby (0.6.4)
    jdg-yajl-ruby (0.5.12)
    oortle-yajl-ruby (0.5.8)
    yajl-ruby (0.6.7)


Or even:

    $ shrepl git
    >> branch
      gh-pages
    * master
    >> tag
    rm
    v0.1.0
    v0.1.1
    v0.1.2
    v0.1.3
    >> tag -d rm
    Deleted tag 'rm'
    >> pwd
    git: 'pwd' is not a git-command. See 'git --help'.

    Did you mean this?
      add

You can also use `%s` to tell shrepl where to stick the input:

    $ shrepl heroku %s --app domainy
    >> info
    === domainy
    Web URL:        http://domainy.heroku.com/
    Git Repo:       git@heroku.com:domainy.git
    Dynos:          1
    Workers:        0
    Repo size:      288k
    Slug size:      4k
    Data size:      0K in 0 table
    Addons:         Piggyback SSL
    Owner:          b****@*******.com


If you have [rlwrap(1)][0] installed you'll automatically get the full
benefits of readline: history, reverse searches, etc.

`shrepl` is meant to wrap programs which accept command line arguments
and print to the standard output. It keeps no state between executed
lines and, as such, cannot be used to replace `irb` or the Python
REPL (for example).


Install
-------

### Standalone

`shrepl` is easily installed as a standalone script:

    export REPL_BIN=~/bin/repl
    curl -s https://github.com/defunkt/repl/raw/latest/bin/repl > $REPL_BIN
    chmod 755 $REPL_BIN

Change `$REPL_BIN` to your desired location and have at! (Just make
sure it's in your `$PATH`.)

Completion
----------

Because `rlwrap` supports completion, `shrepl` does too. Any file in
`~/.repl` matching the name of the command you start `shrepl` with will
be used for completion.

For instance, a file named `~/.repl/redis-cli` containing "get set
info" will cause "get", "set", and "info" to be tab completeable at
the `shrepl redis-cli` prompt.

The directory searched for completion files can be configured using
the `REPL_COMPLETION_DIR` environment variable.

See the [repl-completion](http://github.com/defunkt/repl-completion)
project for a few common, pre-rolled completion files.


Configuration
-------------

The following environment variables affect `shrepl`'s behavior:

`REPL_PROMPT`:
    the prompt to display before each line of input. defaults to >>

`REPL_COMPLETION_DIR`:
    directory in which completion files are kept


Authors
-------

Chris Wanstrath :: chris@ozmm.org :: @defunkt
joh6nn :: joh6nn@joh6nn.com


[0]: http://utopia.knoware.nl/~hlub/rlwrap/


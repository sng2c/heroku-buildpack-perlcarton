Heroku buildpack: Perl/Carton
=============================

This is a Heroku buildpack that runs any Carton based web applications.
Even for Dokku.

Usage
-----

Example usage:

    $ ls
    .env
    cpanfile
    cpanfile.snapshot
    app.psgi
    lib/
    vendor/
    Procfile
    
    $ cat cpanfile
    requires 'Plack', '1.0000';
    requires 'DBI', '1.6';

    $ cat Procfile
    # PERL5LIB=local/lib/perl5 is for compatiblity to Dokku.
    web: PERL5LIB=local/lib/perl5 carton exec starman --preload-app --port \$PORT

    $ cat .env
    # custom buildpack url for Dokku
    export BUILDPACK_URL=https://github.com/sng2c/heroku-buildpack-perlcarton.git

    $ heroku create --stack cedar --buildpack https://github.com/sng2c/heroku-buildpack-perlcarton.git

    $ git push heroku master
    ...
    -----> Heroku receiving push
    -----> Fetching custom buildpack
    -----> Perl/Carton app detected
    ...

The buildpack will detect that your app has a `vendor` in the root.

Libraries
---------

Dependencies can be declared using `cpanfile` (recommended) or more traditional `Makefile.PL`, `Build.PL` and `META.json` (whichever you can install with `cpanm --installdeps`), and the buildpack will install these dependencies using [cpanm](http://cpanmin.us) into `./local` directory.


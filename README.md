# NAME

Dist::Zilla::Plugin::Test::Pod::Coverage::Configurable - dzil pod coverage tests with configurable parameters

# VERSION

version 0.03

# SYNOPSIS

    [Test::Pod::Coverage::Configurable]
    class = Pod::Coverage::Moose
    trustme = Dist::Some::Module => qr/^(?:foo|bar)$/
    trustme = Dist::Some::Module => qr/^foo_/
    trustme = Dist::This::Module => qr/^bar_/
    skip = Dist::Other::Module
    skip = Dist::YA::Module
    skip = qr/^Dist::Foo/

# DESCRIPTION

This is a [Dist::Zilla](https://metacpan.org/pod/Dist::Zilla) plugin that creates a POD coverage test for your
distro. Unlike the plugin that ships with dzil in core, this one is quite
configurable. The coverage test is generated as `xt/release/pod-coverage.t`.

[Test::Pod::Coverage](https://metacpan.org/pod/Test::Pod::Coverage) `1.08`, [Test::More](https://metacpan.org/pod/Test::More) `0.88`, and
[Pod::Coverage::TrustPod](https://metacpan.org/pod/Pod::Coverage::TrustPod) will be added as `develop requires` dependencies.

# NAME

Dist::Zilla::Plugin::Test::Pod::Coverage::Configurable - a configurable release test for Pod coverage

# CONFIGURATION

This plugin accepts the following configuration options

## class

By default, this plugin uses [Pod::Coverage::TrustPod](https://metacpan.org/pod/Pod::Coverage::TrustPod) to run its tests. You
can provide an alternate class, such as [Pod::Coverage::Moose](https://metacpan.org/pod/Pod::Coverage::Moose). If you
provide a class then the generate test file will create a subclass of the
class you provide and [Pod::Coverage::TrustPod](https://metacpan.org/pod/Pod::Coverage::TrustPod).

This test can be configured by providing `trustme`, `skip`, and `class`
parameters in your `dist.ini` file.

Since this test always uses [Pod::Coverage::TrustPod](https://metacpan.org/pod/Pod::Coverage::TrustPod), you can use that to
indicate that some subs should be treated as covered, even if no documentation
can be found, you can add:

    =for Pod::Coverage sub_name other_sub this_one_too

## skip

This can either be a plain module name or a regex of the form `qr/.../`. Any
modules defined here will be skipped entirely when testing POD coverage.

## trustme

This parameter allows you to specify regexes for methods that should be
considered coverage on a per-module basis. The parameter is provided in the
form `Module::Name => qr/^regex/`. You can include the same module name
multiple times.

# AUTHOR

Dave Rolsky <autarch@urth.org>

# COPYRIGHT AND LICENSE

This software is Copyright (c) 2014 - 2015 by Dave Rolsky.

This is free software, licensed under:

    The Artistic License 2.0 (GPL Compatible)

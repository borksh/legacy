# Bork legacy assertion types

![Test status](https://github.com/borksh/legacy/workflows/Test/badge.svg)
![FreeBSD test status](https://img.shields.io/cirrus/github/borksh/legacy?label=FreeBSD&logo=freebsd)

Here is an index of **officially deprecated** Bork assertion types and
documentation on how to use them. These **do not ship with** Bork, and are only
available from this repository.

Please note that legacy types are not routinely maintained by Bork's core
maintainers. Pull requests are welcome on this repository, but there are **no
guarantees** that the types included here will still work, or will not have bugs
or security vulnerabilities. Generally speaking, a type makes it into the legacy
repository if the upstream utility to which it corresponds is deprecated or
otherwise no longer recommended for use.

## How to use these types

This repository is structured identically to the
[main Bork repository](https://github.com/borksh/bork), meaning you can 'drop
in' the legacy types over the top of an existing Bork installation (which is
roughly how the tests are done in CI). If you don't want to do this, you can
simply download the type files you are interested in from the [types/](types/)
directory, and register them with Bork as though they were custom types like so:

```bash
register pipsi.sh
```

You can then use them in your scripts exactly like any other Bork assertion.

## Contributing

Please see the [contributors' guide](CONTRIBUTING.md) for further information
about this repository, but in short, the usual rules of contributing to GitHub
repositories apply:

1. Fork it
2. Create your feature branch: `git checkout -b feature/my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin feature/my-new-feature`
5. Submit a pull request

Pull requests are subject to (generally automated) review. We will not accept
pull requests whose tests fail or where [Danger](https://danger.systems)
requests changes. This is a low-maintenance repository, and we trust our
automated tools. There is more information about this approach in the
[contributors' guide](CONTRIBUTING.md).

## License

[Apache License 2.0](LICENSE)

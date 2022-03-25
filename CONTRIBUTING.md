# Bork legacy type contributor's guide

Hi there! Thank you for your interest in contributing to Bork's legacy type
repository. We appreciate your assistance, as legacy types are officially
deprecated by Bork core maintainers, and so can't be kept in good working order.

That said, it is worth saying: **please consider if contributing to this
repository is really what you want to do**. Generally speaking, a type makes it
into the legacy repository if the upstream utility to which it corresponds is
deprecated or otherwise no longer recommended for use. Your workflow may require
this, and that's fine — we have all been cursed to use legacy software before
now — but this notice should serve as a reminder that that's what you are doing.
If you have control over your own environment, it may be worth considering
updating your workflow rather than using legacy assertions.

## Once you're sure you want to be here

The usual rules of contributing to GitHub repositories apply:

1. Fork it
2. Create your feature branch: `git checkout -b feature/my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin feature/my-new-feature`
5. Submit a pull request

Pull requests are subject to (generally automated) review. We will not accept
pull requests whose tests fail or where [Danger](https://danger.systems)
requests changes. This is a low-maintenance repository, and we trust our
automated tools. More on that below.

## Contribution guidelines

These are copied from [Bork core](https://github.com/borksh/bork), and apply to
assertion types in here as well.

1. Prefer clarity of intent over brevity. Bash can be an obtuse language, but it
   doesn't *have* to be. Many people have said bork has some of the clearest
   bash code they've ever seen, and that's a standard to strive for.

2. Favor helper abstractions over arbitrary platform-specific checks. See [`md5cmd`](https://github.com/borksh/bork/blob/main/lib/helpers/md5cmd.sh), [`http`](https://github.com/borksh/bork/blob/main/lib/helpers/http.sh), and [`permission_cmd`](https://github.com/borksh/bork/blob/main/lib/helpers/permission_cmd.sh), and look at how they're used. Remember `lib` files/functions in Bork core will be available to you in legacy types (and indeed any custom type).

3. Types are independent, stateless, and atomic. Do not attempt to maintain a
   cache in a type file unless you're talking to the network. An assertion is
   the *whole* of the assertion — don't attempt to create a multi-stage
   assertion type that depends on maintaining state. Find a way to express the
   whole of the assertion in one go.

4. Leave Dependency Management to the user. Is a needed binary not installed for
   a type? Return `$STATUS_FAILED_PRECONDITION` in your status check. Let the
   user decide the best way to satisfy any dependencies.

5. There will be a handful of types in here that are **just going to be
   broken**, because of upstream changes to software they interact with. Leave
   them be, in case someone comes looking for them; if they pass the automated
   tests, there's a good chance it worked when it was written. That doesn't mean
   don't fix things where it is possible — this is more about not removing stuff
   from this repository unless there is a good reason to.

## Automated testing and checks

We use [bats](https://github.com/bats-core/bats-core) to run automated Bash
tests on types, and [Danger](https://danger.systems) to do some basic checks on
things like code style and PR metadata. Keeping this repository ticking over is
designed to be low effort for Bork maintainers, so as much as possible is
automated to allow for minimal human intervention. More time spent here equals
less time spent on core Bork. As a result, we will not accept pull requests
where any of the following are true:

* The tests fail on either Linux or macOS (both are tested by CI). The only
  exception to this is if the tests fail for a reason unrelated to your
  contribution, in which case we will re-run them.

* Danger gives you a rejected review on your pull request. Please see the
  comment from @github-actions on your PR and act accordingly before
  making changes or resubmitting.

* You do not include tests with new or updated code.

* Your code requires an older version of Bork than the current `main` branch of
  the core repository (against which it will be tested).

These requirements are not to dissuade you from contributing, but to ensure that
time spent on legacy code is spent wisely.

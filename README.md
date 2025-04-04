[![PyPI](https://img.shields.io/pypi/v/afkafe)](https://pypi.org/project/afkafe)
[![Downloads](https://static.pepy.tech/badge/afkafe)](https://pepy.tech/project/afkafe)

# AFKafé

AFKafé is a simple service that uses pynput to monitor your system activity. If you idle for too long, AFKafé assumes you have entered a catatonic state due to caffeine deprivation and quickly orders a random bag of coffee (but never decaf) from [terminal.shop](https://terminal.shop). I pray it reaches you in time.

## Installation

The best way to install is with [pipx](https://github.com/pypa/pipx):

```
$ pipx install afkafe
```

## Usage

First, you'll need to store your terminal.shop access token in the environment variable `$TERMINAL_BEARER_TOKEN`. You should also make sure that the associated account at terminal.shop (or dev.terminal.shop) already has payment and address information saved. Now you can run the service:

```
$ afkafe --dev --verbose 5
```

Here, we're running with an idle timeout of 5 seconds. That's pretty low unless you're a 10x developer, so we're also running in the dev environment to avoid needlessly giving money to startup grifters. Finally, we're using the `--verbose` flag so you can ensure that keyboard and mouse events are being detected by the service. If everything is working correctly, you should see something like this as you use your mouse/keyboard:

```
13:22:51: Big dict entered the void (of the logging config)
13:22:55: Received event (637, 477, False)
13:22:55: Received event (636, 478, False)
13:22:55: Received event (634, 488, False)
13:22:55: Received event (627, 505, False)
13:22:55: Received event (609, 523, False)
13:22:55: Received event (569, 545, False)
13:22:55: Received event (519, 575, False)
a13:22:56: Received event ('a', False)
s13:22:56: Received event ('s', False)
d13:22:56: Received event ('d', False)
k13:22:56: Received event ('k', False)
f13:22:56: Received event ('f', False)
13:22:56: Received event ('j', False)
j13:22:56: Received event ('a', False)
13:22:59: Received event (642, 617, <Button.left: 1>, True, False)
13:22:59: Received event (642, 617, <Button.left: 1>, False, False)
13:23:00: Received event (642, 617, <Button.right: 3>, True, False)
13:23:00: Received event (642, 617, <Button.right: 3>, False, False)
13:23:00: Received event (642, 617, <Button.right: 3>, True, False)
13:23:00: Received event (642, 617, <Button.left: 1>, True, False)
13:23:00: Received event (642, 617, <Button.right: 3>, False, False)
13:23:00: Received event (642, 617, <Button.left: 1>, False, False)
13:23:01: Received event (643, 618, False)
13:23:01: Received event (645, 618, False)
13:23:01: Received event (<Key.ctrl: <65507>>, False)
13:23:01: Received event ('c', False)
```

And if you're idle for over 5 seconds, you should see this:

```
13:25:10: User needs caffeine!
13:25:11: Selected bag artisan out of desperation.
13:25:13: Placed order ord_01JQ78T9TFSEFF96EB8VG120RB
```

After ordering, the service exits since a single bag should be enough to keep you running for a while.

Now that everything is working, you should configure the script to run in the background. There are many ways to do this, but one way is to add this line to your `.xinitrc` file if you're using `startx`:

```
~/.local/bin/afkafe &
```

By default, the idle time is 30 minutes before coffee is ordered. That should be appropriate for all you normie programmers, Twitch chatters, and Reddit users out there. Enjoy your coffee and boosted productivity!

## Supported platforms

AFKafé has only been tested on Linux with Xorg (Wayland is not supported!), but it should work on any platform that [pynput works on](https://pynput.readthedocs.io/en/latest/limitations.html).

# Pulse

![Pulse icon](./pulse_icon.png)

### *Give your events a Pulse!*

---

Pulse is a lightweight but feature rich signal / event framework for GameMaker, designed to be your new go to for decoupling game logic. Instead of hard-wiring everything together with direct function calls and global variables, you fire signals into Pulse and let whoever cares listen in. Start with a simple global bus, then layer on filters, priorities, queues, and queries when you need more control.

This repository is for the Pulse framework landing page and issue tracker.

## Features at a glance

* Clean, minimal API that drops into any GameMaker project with just a few calls.
* Global signal bus for quick wins, plus support for multiple independent busses.
* Simple subscribe / send workflow with `PulseSubscribe` and `PulseSend`.
* One-shot listeners via `PulseSubscribeOnce` for "do this exactly once" moments.
* Optional `from` filters so listeners can target specific senders.
* Tags and priorities for more advanced routing and ordering.
* Queued events with `PulsePost` / `PulseFlushQueue` so you can process signals at controlled times.
* Cancellable events so higher-priority listeners can "consume" a signal and stop propagation.
* Query API (`PulseQuery`, `PulseQueryAll`, `PulseQueryFirst`) so listeners can vote on results instead of just reacting.
* Introspection helpers (`PulseCount`, `PulseCountFor`, `PulseDump`, `PulseDumpSignal`) for debugging and tools.
* Designed to play nicely with Echo, my debug logging framework, if you want extra visibility into what your signals are doing.

## Quick start

A minimal example: one signal, one listener, one sender.

First, define a signal identifier:

```js
// sig_pulse.gml
#macro SIG_DAMAGE_TAKEN 0
```

In your player object, subscribe to the signal:

```js
/// obj_player Create
PulseSubscribe(id, SIG_DAMAGE_TAKEN, function(_data) {
    var _amount = is_struct(_data) ? _data.amount : _data;
    hp -= _amount;
});
```

Somewhere else, send the signal when damage happens:

```js
/// obj_enemy: when it hits the player
var _payload = { amount: 5 };
PulseSend(SIG_DAMAGE_TAKEN, _payload, id);
```

That is the core loop:

* Define a signal.
* Subscribe a listener.
* Send the signal.

From there you can layer on:

* `PulseSubscribeOnce` for one-shot reactions.
* `PulsePost` / `PulseFlushQueue` for queued processing.
* `PulseCount` / `PulseDump` when you want to see what is wired up.

For more advanced examples (custom busses, queries, cancellation, grouping subscriptions, etc) see the full documentation.

## Documentation

Full online docs are available here:

### Pulse docs:

[https://refreshertowel.github.io/docs/pulse/](https://refreshertowel.github.io/docs/pulse/)

## Where to buy

Pulse is available on itch.io:

Itch page:
Pulse (not up yet)

## Bug reports and feature requests

The best place to report bugs or request features is the GitHub Issues page:

Issues:
[https://github.com/RefresherTowel/Pulse/issues](https://github.com/RefresherTowel/Pulse/issues)

If you are not comfortable using GitHub, you can also post in the [**Pulse channel on the RefresherTowel Games Discord**](https://discord.gg/acAqBcYHgV) and I can file an issue for you.

## License

Pulse is a paid framework. The license terms for using it in your projects are in:

[LICENSE_Pulse.txt](LICENSE_Pulse.txt)

In short: it is licensed per developer seat, you can use it in unlimited games (free or commercial), but you cannot redistribute the framework source itself.

## Credits and third party assets

Example projects for Pulse may use third party art assets (for example, Kenney assets from kenney.nl). These are provided under their own licenses and are not covered by the Pulse framework license. See the example project PulseCredits note for details.

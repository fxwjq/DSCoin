# DSCoin Guide

*work in progress*

This is a more in depth description of the DSCoin core contracts. 


## Tooling

- dapp.tools
- solc v0.5.0
- tests use ds-test and are in files ending .t.sol


## Units



## Code style

This is obviously opinionated and you may even disagree, but here are
the considerations that make this code look like it does:

- Distinct things should have distinct names ("memes")

- Lack of symmetry and typographic alignment is a code smell.

- Inheritance masks complexity and encourages over abstraction, be
  explicit about what you want.

- In this modular system, contracts generally shouldn't call or jump
  into themselves, except for math. Again, this masks complexity.


### Rate

The ilk quantity `rate` define the ratio of exchange
between un-encumbered and encumbered Debt.

This quantity allows for manipulation of debt balances
across a whole Ilk.

Debt can be seized or injected into an ilk using `fold(i, u, rate)`,
which increases the `dai` balance of the user `u` by increasing the
encumbered debt balance of all urns in the ilk by the ratio `rate`.

## CDP Interface

The `Vat` contains risk parameters for each `ilk`:

- `spot`: the maximum amount of Dai drawn per unit collateral
- `line`: the maximum total Dai drawn

And a global risk parameter:

- `Line`: the maximum total Dai drawn across all ilks

The `Vat` exposes the public function:

- `frob(ilk, dink, dart)`: manipulate the callers CDP in the given `ilk`
  by `dink` and `dart`, subject to the risk parameters

## Liquidation Interface

The companion to CDP management is CDP liquidation, which is defined via
the `Cat`.

The `Cat` contains liquidation parameters for each `ilk`:

- `flip`: the address of the collateral liquidator
- `chop`: the liquidation penalty
- `lump`: the liquidation quantity

The `Cat` exposes two public functions

- `bite(ilk, urn)`: mark a specific CDP for liquidation
- `flip(n, wad)`: initiate liquidation



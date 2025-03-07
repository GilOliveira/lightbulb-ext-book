# Neon

**This library is a maintained fork of [lightbulb-ext-neon](https://github.com/neonjonn/lightbulb-ext-neon) made by NeonJonn**

**Neon** is an add-on for [Lightbulb](https://github.com/tandemdude/hikari-lightbulb/) making it easier to handle component interactions.

## Installation

```bash
pip install git+https://github.com/GilOliveira/lightbulb-ext-book.git
```

## Documentation

[ReadTheDocs](https://lightbulb-neon.readthedocs.io/en/latest/)

## Usage

```python
from lightbulb.ext import neon

class Menu(neon.ComponentMenu):
    @neon.button("earth", "earth_button", hikari.ButtonStyle.SUCCESS, emoji="\N{DECIDUOUS TREE}")
    async def earth(self, button: neon.Button) -> None:
        await self.edit_msg(f"{button.emoji} - {button.custom_id}")

    @neon.option("Water", "water", emoji="\N{DROPLET}")
    @neon.option("Fire", "fire", emoji="\N{FIRE}")
    @neon.select_menu("sample_select_menu", "Pick fire or water!")
    async def select_menu_test(self, values: list) -> None:
        await self.edit_msg(f"You chose: {values[0]}!")

    @neon.button("Wind", "wind_button", hikari.ButtonStyle.PRIMARY, emoji="\N{WIND BLOWING FACE}\N{VARIATION SELECTOR-16}")
    @neon.button("Rock", "rock_button", hikari.ButtonStyle.SECONDARY, emoji="\N{MOYAI}")
    @neon.button_group()
    async def wind_rock(self, button: neon.Button) -> None:
        await self.edit_msg(f"You pressed: {button.custom_id}")

    @neon.on_timeout(disable_components=True)
    async def on_timeout(self) -> None:
        await self.edit_msg("\N{ALARM CLOCK} Timed out!")

@bot.command
@lightbulb.command("neon", "Check out Neon's component builder!")
@lightbulb.implements(lightbulb.SlashCommand, lightbulb.PrefixCommand)
async def neon_command(ctx: lightbulb.Context) -> None:
    menu = Menu(ctx, timeout=30)
    resp = await ctx.respond("Check out Neon's component builder!", components=menu.build())
    await menu.run(resp)
```

## Contributors

* [thomm.o](https://github.com/tandemdude) - [Refactor, improve code, mypy compliance](https://github.com/neonjonn/lightbulb-ext-neon/pull/1)
* [Coler6gamer](https://github.com/Coler6gamer) - [Removed blocking return statement](https://github.com/neonjonn/lightbulb-ext-neon/pull/2)

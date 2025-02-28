asyncclick
==========

What's AsyncClick?
------------------

AsyncClick ist a fork of Click that works well with trio or asyncio.

Click is a Python package for creating beautiful command line interfaces
in a composable way with as little code as necessary. It's the "Command
Line Interface Creation Kit". It's highly configurable but comes with
sensible defaults out of the box.

It aims to make the process of writing command line tools quick and fun
while also preventing any frustration caused by the inability to
implement an intended CLI API.

AsyncClick in four points:

-   Arbitrary nesting of commands
-   Automatic help page generation
-   Supports lazy loading of subcommands at runtime
-   Seamlessly use async-enabled command and subcommand handlers

Installing
----------

Install and update using `pip`_:

.. code-block:: text

    $ pip install asyncclick

AsyncClick supports Python 3.7 and newer, and PyPy3.

.. _pip: https://pip.pypa.io/en/stable/getting-started/

A Simple Example
----------------

.. code-block:: python

    import anyio
    import asyncclick as click
    # You can use all of click's features as per its documentation.
    # Async commands are supported seamlessly; they just work.
    
    @click.command()
    @click.option("--count", default=1, help="Number of greetings.")
    @click.option("--name", prompt="Your name", help="The person to greet.")
    async def hello(count, name):
        """Simple program that greets NAME for a total of COUNT times."""
        for x in range(count):
            if x: await anyio.sleep(0.1)
            click.echo(f"Hello, {name}!")

    if __name__ == '__main__':
        hello(_anyio_backend="trio")  # or asyncio

    # You can use your own event loop:
    #    import anyio
    #    async def main():
    #        await hello.main()
    #    if __name__ == '__main__':
    #        anyio.run(main)
    # This is useful for testing.

.. note::
    AsyncClick automagically starts an anyio event loop and runs your
    code asynchronously. You don't need to use `anyio.run`.

.. code-block:: text

    $ python hello.py --count=3
    Your name: Click
    Hello, Click!
    Hello, Click!
    Hello, Click!


Donate
------

The Pallets organization develops and supports Click and other popular
packages. In order to grow the community of contributors and users, and
allow the maintainers to devote more time to the projects, `please
donate today`_.

.. _please donate today: https://palletsprojects.com/donate

The AsyncClick fork is maintained by Matthias Urlichs <matthias@urlichs.de>.
It's not a lot of work, so if you'd like to motivate me, donate to the
charity of your choice and tell me that you've done so. ;-)

Links
-----

``AsyncClick`` is sufficiently minimal to not have its own web page.

-   Code: https://github.com/python-trio/asyncclick

These links point to the original, non-async-enabled, version of ``Click``.

-   Website: https://palletsprojects.com/p/click/
-   Documentation: https://click.palletsprojects.com/
-   Changes: https://click.palletsprojects.com/changes/
-   PyPI Releases: https://pypi.org/project/click/
-   Source Code: https://github.com/pallets/click
-   Issue Tracker: https://github.com/pallets/click/issues
-   Chat: https://discord.gg/pallets

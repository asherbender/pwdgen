pwdgen
================================================================================

Generate random passwords.

Passwords are generated by sampling bytes from `/dev/random
<https://en.wikipedia.org/wiki//dev/random>`_ and mapping this random data to a
character set. The advantage of using ``/dev/random`` is that it can provide
high-quality random numbers by collecting environmental noise from device
drivers and other resources. ``/dev/random stores`` this random data in an
entropy pool of 4096 bits (512 Bytes). An estimate of the number of bits of
noise in the entropy pool is maintained. When enough bits of entropy have been
collected, random bytes can be read from the pool, depleting the resource. Once
the pool is exhausted, ``/dev/random`` will block until enough noise has been
collected to provide new random bytes. To ensure sufficient entropy is available
for the system, ``pwdgen`` will not sample bytes until
``/proc/sys/kernel/random/entropy_avail`` registers a minimum level of entropy.


Installation
--------------------------------------------------------------------------------

This code supports installation using pip (via `setuptools
<https://pypi.python.org/pypi/setuptools>`_). To install from the git
repository:

.. code-block:: bash

    git clone https://github.com/asherbender/pwdgen
    cd pwdgen
    sudo pip install .

Once installed, the command ``pwdgen`` is available from the command-line. The
script is typically installed in

.. code-block:: bash

    /usr/local/bin/

To uninstall the package:

.. code-block:: bash

    pip uninstall pwdgen

Dependencies
--------------------------------------------------------------------------------

``pwdgen`` can only work on Unix-like operating systems which provide the
``/dev/random`` and ``/proc/sys/kernel/random/entropy_avail`` resources.


Usage
--------------------------------------------------------------------------------

To generate a random password:

.. code-block:: bash

    pwdgen --length 16

Example output:

::

    Number of symbols:  62
    Password length:    16
    Permutations:       10^28
    Entropy per symbol:  5.954 bits
    Total entropy:      95.267 bits

    Collecting environmental noise collected from device drivers and other
    sources. It is a good idea to perform some other action (type on the
    keyboard, move the mouse, utilize the disks) during the prime
    generation; this gives the random number generator a better chance to
    gain enough entropy.

    Entropy available: 0198 bits,  Characters sampled: 16

    aA2oRq3qQlo8D5KX


Additional functionality is documented in ``pwdgen --help``:

::

    usage: pwdgen [-h] [-L <int>] [-u] [-l] [-n] [-p] [--include <string>]
                  [--exclude <string>] [--list] [-m <int>] [-q]

    Generate random passwords.

        Passwords are generated by sampling bytes from /dev/random and mapping this
        random data to a character set. The advantage of using /dev/random is that
        it can provide high-quality random numbers by collecting environmental
        noise from device drivers and other resources. /dev/random stores this
        random data in an entropy pool of 4096 bits (512 Bytes). An estimate of the
        number of bits of noise in the entropy pool is maintained. When enough bits
        of entropy have been collected, random bytes can be read from the pool,
        depleting the resource. Once the pool is exhausted, /dev/random will block
        until enough noise has been collected to provide new random bytes. To
        ensure sufficient entropy is available for the system, pwdgen will not
        sample bytes until /proc/sys/kernel/random/entropy_avail registers a
        minimum level of entropy.

    optional arguments:
      -h, --help            show this help message and exit
      -L <int>, --length <int>
                            length of password (default=24)
      -u, --upper           Exclude uppercase letters: ABCDEFGHIJKLMNOPQRSTUVWXYZ
      -l, --lower           Exclude lowercase letters: abcdefghijklmnopqrstuvwxyz
      -n, --numeric         Exclude numeric characters: 0123456789
      -p, --punctuation     Include punctuation characters:
                            !"#$%&'()*+,-./:;<=>?@[\]^_`{|}~
      --include <string>    Specify which characters will be used for random
                            password generation (--upper, --lower, --numeric and
                            --punctuation).
      --exclude <string>    Specify which characters will be excluded from random
                            password generation.
      --list                Print characters available for random password
                            generation and exit.
      -m <int>, --min <int>
                            Minimum level in entropy pool before sampling occurs
                            (default=128).
      -q, --quiet           Suppress output to stdout.


License
--------------------------------------------------------------------------------

This code is licensed under the `GNU General Public License Version 3 (GPLv3)
<https://gnu.org/licenses/gpl.html>`_.

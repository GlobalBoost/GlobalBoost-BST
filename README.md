Globalboost integration/staging tree
================================

http://www.globalboost.org

Copyright (c) 2009-2013 Bitcoin Developers
Copyright (c) 2011-2013 Litecoin Developers
Copyright (c) 2014 Globalboost Developers

What is Globalboost?
----------------

Globalboost is a version of Bitcoin using scrypt as a proof-of-work algorithm.
 - 30 seconds block targets
 - 1 Billion total coins
 
 - base58.h PUBKEY_ADDRESS = 58, // Globalboost addresses start with G
  - src/protocol.h port: return testnet ? 12369 : 12368; 
 - src/init.cpp " -port=<port>           " + _("Listen for connections on <port> (default: 12368 or testnet: 12369)") + "\n" +
 - src/bitcoinrpc.cpp    return GetBoolArg("-testnet", false) ? 12367 : 12366;
 - src/main.h max coin and dPriority
 - Set the genesis block in src/main.cpp LoadBlockIndex paraphrase (pszTimestamp) to any recent news phase. get the latest unix time (do a google), and put in block.nTime. set any nNonce (doesn't really matter)
 - src/base58.h PUBKEY_ADDRESS = 28, // Globalboost addresses start with G
 - src/sendcoinsentry.cpp     ui->payTo->setPlaceholderText(tr("Enter a Globalboost address (e.g. GcdLutynys98Avs51xJmn7whajD9YSro8j)"));
 - change example in signverifymessagedialog.cpp     ui->addressIn_SM->setPlaceholderText(tr("Enter a Globalboost address (e.g. GcdLutynys98Avs51xJmn7whajD9YSro8j)"));
 - Checkpoint: you want to disable the checkpoint check initially, otherwise you may get stuck. You have multiple ways to disable it, my way is: open checkpoints.cpp there are 3 functions, comment out the normal return, and make them return either true, 0, or null.


For more information, as well as an immediately useable, binary version of
the Globalboost client sofware, see http://www.globalboost.org.

License
-------

Globalboost is released under the terms of the MIT license. See `COPYING` for more
information or see http://opensource.org/licenses/MIT.

Development process
-------------------

Developers work in their own trees, then submit pull requests when they think
their feature or bug fix is ready.

If it is a simple/trivial/non-controversial change, then one of the Globalboost
development team members simply pulls it.

The patch will be accepted if there is broad consensus that it is a good thing.
Developers should expect to rework and resubmit patches if the code doesn't
match the project's coding conventions (see `doc/coding.txt`) or are
controversial.

The `master` branch is regularly built and tested, but is not guaranteed to be
completely stable. [Tags](https://github.com/GlobalBoost/GlobalBoost/tags) are created
regularly to indicate new official, stable release versions of Globalboost.

Testing
-------

Testing and code review is the bottleneck for development; we get more pull
requests than we can review and test. Please be patient and help out, and
remember this is a security-critical project where any mistake might cost people
lots of money.

### Automated Testing

Developers are strongly encouraged to write unit tests for new code, and to
submit new unit tests for old code.

Unit tests for the core code are in `src/test/`. To compile and run them:

    cd src; make -f makefile.unix test

Unit tests for the GUI code are in `src/qt/test/`. To compile and run them:

    qmake GLOBALBOOST_QT_TEST=1 -o Makefile.test globalboost-qt.pro
    make -f Makefile.test
    ./globalboost-qt_test


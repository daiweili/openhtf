DISCLAIMER: This is not an official Google product.


# OpenHTF
OpenHTF is an open-source hardware testing framework targeting manufacturing
use cases, but hopefully general enough to be useful in a variety of hardware
testing scenarios.


## Nomenclature
OpenHTF uses certain nomenclature internally for several of its core concepts.
Some of the more important terms are listed here for clarity.


### DUT (Device Under Test)
DUT refers to an individual piece of hardware being evaluated, exercised, or
tested.


### Test
The top-level abstraction that OpenHTF deals with is the "test". A test is just
a series of steps performed on/with a DUT, usually along with some
data-gathering or measurement steps. In the OpenHTF paradigm, tests are
expressed as regular python programs (.py files). That way they're as
straightforward as possible to read and write. This also gives you the
flexibility to do anything in a test that you could normally do in python.
Superficially, what distinguishes an OpenHTF test from any other python program
is that the OpenHTF test imports the openhtf package, and calls its top-level
execute_test function. From there, OpenHTF manages the setup, execution, and
teardown of the test, keeps track of the any gathered, and provides a pass/fail
result.


### Testrun
A testrun is a single start-to-finish execution of a single test.


### Cell
Cells are multiple concurrent copies of the same test being run and executed by
the same instance of OpenHTF. In practice, most tests only have a single cell.
Sometimes, however, a test fixture is set up such that having multiple cells
makes sense. Since all multi-cell use cases can in theory be reduced to single-
cell tests, deprecation of multi-cell support is being stronly considered.


### Test Phase
OpenHTF tests are broken down into logical blocks called phases. Phases are no
more than normal python callables (usually functions) combined with the needed
metadata.


### Parameter
In OpenHTF parlance, a parameter is any value that is being measured during the
course of a testrun. Usaually, parameters are declared along with a spec that
desribes what consitites a "passing" score for that value. If OpenHTF finishes
the testrun and one or more paramters were out of spec, the result of the whole
testrun will be considered a "fail".


### Capability
The essence of an OpenHTF test is to interact with a DUT to exercise it in
various ways and observe the result. Sometimes this is done by communicating
directly with the DUT, and other times it's done by communicating with a piece
of test equipment to which the DUT is attached in some way. A capability is a
piece of code written to enable OpenHTF to interact with a particular type of
hardware, whether that be a DUT itself or a piece of test equipment. OpenHTF
comes packaged with a growing collection of useful capabilites, but supports the
creation of custom capabilities as well.

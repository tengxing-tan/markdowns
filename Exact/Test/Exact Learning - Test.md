unit test vs integration test
unit test stand for isolation, white-box, less cost, stupid and simple
integration test stand for combination, black-box, reply on database or other test case. 
tester workflow: unit test, then integration test, then system test. 

test flow
classinit,  constructor, testinit, testmethod, testcleanup, dispose
classcleanup

cleanup is important to make sure one test does not affect another test


checklist why test failed
- [ ] too quick, time bomb
- [ ] exception in the middle, no proper handling. the rest of the test won't run
- [ ] pollute database
- [ ] missing hosting setting
- [ ] hanging transaction/ nested transaction

takeaway
- [ ] Do not use hostingStub
- [ ] Avoid cache
- [ ] Do not use conditional statement in test code
- [ ] Do not use constructor for your test class 
- [ ] Do not use IDisposable for your test class 

Dispose IDisposable
- EolTestContext
- IEnvironment
- EdlConnection
- EdlTransaction
- SystemClock


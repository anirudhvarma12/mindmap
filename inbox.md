# Inbox

## Marble Testing
Things learned
1. Each expectObservable needs to be in a new scheduler, otherwise the same time continues.
2. An observable made from of that emits one value and completes immediately is `(a|)`.
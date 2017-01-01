# BDD

BDD是TDD的另外一种形式，优点是可以把测试代码当作文档来读。我知道最典型的案例是Reactive Cocoa\
的BDD代码。

[Reactive Cocoa BDD 案例](https://github.com/ReactiveCocoa/ReactiveCocoa/blob/v3.0-RC.1/ReactiveCocoaTests/Objective-C/RACSubjectSpec.m)

RAC BDD 片段

```
qck_it(@"should not send any values to new subscribers if none were sent originally", ^{
			[subject sendCompleted];

			__block BOOL nextInvoked = NO;
			[subject subscribeNext:^(id x) {
				nextInvoked = YES;
			}];

			expect(@(nextInvoked)).to(beFalsy());
		});
```

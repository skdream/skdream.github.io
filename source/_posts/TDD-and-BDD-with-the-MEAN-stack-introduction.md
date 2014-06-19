title: 用TDD和BDD来测试MEAN的介绍
date: 2014-02-23 10:42:27
tags: test
---

原文 http://attackofzach.com/tdd-bdd-mean-part1/

随着[MEAN stack](http://thecodebarbarian.wordpress.com/2013/04/29/easy-web-prototyping-with-mongodb-and-nodejs/)越来越多的被使用，出现了大量的测试MEAN方面的策略。随着我深入研究服务器端和浏览器端的自动化测试MEAN stack的方案,我发现很难找到一些关于如何搭建支持[mockist style](http://martinfowler.com/articles/mocksArentStubs.html#ClassicalAndMockistTesting)的测试驱动的环境的资料或建议。许多作者提供了一些轻量级的建议，但那些建议往往是过去的一些解决方案。我希望能制定一个满足如下条件的工具
* 自动化
* mocklist 单元测试
* BDD/ATDD 测试
* End-To-End系统的测试

如果你想研究这技术的实现代码，我建了个[github项目](https://github.com/zpratt/thoughtsom)来描述这种技术。

下面我假设你已经了解MongoDB和nodejs。如果你不了解，可以查看下 [a vagrant solution](https://github.com/cmoudy/mean-vagrant)和 [mean.io](http://www.mean.io/)。

我的目标之一是尝试找到既能在服务器端也能在浏览器端都能工作的工具。同时我也花了很多精力来研究自动化，因此我的目标是避免人工打开浏览器来执行测试。事实证明这个目标是充满挑战的。xUnit-side的测试和BDD-side的测试的目标是类似的。但是我们的要坚持以前的目标。

让我来介绍下能在前端和后端都工作的很好的工具：
* [Grunt](http://gruntjs.com/) - 任务管理
* [Mocha](http://visionmedia.github.io/mocha/) - 测试框架
* [Chai](http://chaijs.com/) - 断言库
* [Sinon](http://sinonjs.org/) - 替代，模拟的瑞士军刀

一些工具要通过一些处理才能在服务器端和浏览器端工作
* [Yadda](https://github.com/acuminous/yadda) - BDD方面与Mocha和Chai工作的很好(在浏览器端使用需要做些小处理，[我现在在做这方面的工作](https://github.com/zpratt/yadda-karma-example))
* [Cucumber-js](https://github.com/cucumber/cucumber-js) - (BDD) 在服务器端工作的很好，但在浏览器端不能工作（主要是缺少karma方面的支持）

最后，一些只能在一端工作的好的：
* [Karma](http://karma-runner.github.io/) - 在浏览器端运行的测试工具
* [karma-browserifast](https://github.com/cjohansen/karma-browserifast) - Karma的浏览器插件，在浏览器中自动的运行Yadda BDD测试时需要它
* [Supertest](https://github.com/visionmedia/supertest) - 一个了不起的测试基于Express（nodejs框架） REST风格的工具
* [CasperJS](http://casperjs.org/) - 测试用户UI交互(能和Yadda一起工作) 

下面会有更多。我计划写至少两篇文章来详细的描述什么是在服务器和浏览器端的测试驱动。目前可以看下我的浏览器端的BDD风格的单元测试的例子,[Github上的Yadda/Karma](https://github.com/zpratt/yadda-karma-example)，以及服务器端BDD风格的单元测试的例子,[thoughtsom](https://github.com/zpratt/thoughtsom)。我计划在写下篇文章之前写更多的浏览器端测试的代码示例。同时，欢迎大家与我交流。

P.S 我了解[Protractor](https://github.com/angular/protractor),但我还没有机会去玩一下它。     
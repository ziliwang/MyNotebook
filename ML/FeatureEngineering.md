### Part I Empirical Analysis of Feature Engineering
#### common Engineered Features

|Name|cName|Math|Decision Tree|NN|SVM|
|---|---|---|---|---|---|
|Counts||$\sum_i^n 1 \ if \ f(x_i) \ else \ 0$|+++|+|+|
|Differences|Minus|$x_1-x_2$|o|+|o |
|Logarithms||$log$|+|o|+|
|Polynomials||$ax^2 + bx +c$|o|+|+|
|Powers|square|$x^2$|o|+|+|
|Powers|square root|$\sqrt{x}$|0|+|+|
|Ratios| |$\frac{x_1}{x_2}$|+++|+++|+++|
|Rational Differences||$\frac{x_2-x_1}{x_4-x_3}$|+++|+++|+++|
|Rational Polynomials||$\frac{1}{ax^2 + bx}$|o|o|o|
|Distance of Quadratic Root|distance between the roots of a quadratic equation|$abs(\frac{-b + \sqrt{b^2-4ac} }{2a} - \frac{-b - \sqrt{b^2-4ac}}{2a})$|+|+|+++|

note:
  - o: little useful
  - +: small useful
  - ++: useful
  - +++: marked useful

suggest: start at ++.
*from Heaton J. An empirical analysis of feature engineering for predictive modeling[C]//SoutheastCon, 2016. IEEE, 2016: 1-6.*

### Mine
incompletion test on those conclusions on real world data:
 - most create feature method on some feature can improve the performance, but reduced on other feature.
 - 小范围内，new created特征数目增加，模型性能增加。但超过这个范围后，模型性能随新建特征增加而降低。这就表明，新建特征的同时也在引进噪音，所以需要将新建特征控制在一定的范围内。

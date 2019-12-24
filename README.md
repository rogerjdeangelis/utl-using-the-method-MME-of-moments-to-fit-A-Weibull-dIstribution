# utl-using-the-method-MME-of-moments-to-fit-A-Weibull-dIstribution
Using the method of moments to fit Weibull dostribution
    StackOverflow: Using the method of moments to fit a Weibull dostribution

    Elegant R code for many distributions and metods?

    graphical output
    https://tinyurl.com/wq97vzr
    https://github.com/rogerjdeangelis/utl-using-the-method-MME-of-moments-to-fit-A-Weibull-dIstribution/blob/master/Weibull.pdf

    github
    https://tinyurl.com/shdcgn9
    https://github.com/rogerjdeangelis/utl-using-the-method-MME-of-moments-to-fit-A-Weibull-dIstribution

    Stackoverflow
    https://tinyurl.com/shdcgn9
    https://stackoverflow.com/questions/59409043/how-to-fit-weibull-distribution-using-mme-method-and-find-the-estimates-in-r

    Profile
    Severin Pappadeux
    https://stackoverflow.com/users/4044696/severin-pappadeux

    Moment matching (MME),
    Quantile matching (QME)
    Maximum goodness-offit estimation (MGE) methods (available only for non-censored data).
    Weighted versions of MLE, MME and QME are available.

    see comments on link
    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    %let alpha=10;
    %let beta=1;

                  ,-    -, Alpha-1  ,-  ,-    -, Alpha -,
            Alpha |   X  |          |   |   X  |        |
    f(x) =  ----- | ---- |      exp | - | ---- |        |
            Beta  | Beta |          |   | Beta |        |
                  `-    -`          `-  `-    -`       -`

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    Fitting of the distribution ' weibull ' by matching moments

    Parameters :

          estimate
    shape 9.910132
    scale 1.002415

    Loglikelihood:  772.526   AIC:  -1541.052   BIC:  -1531.236

    Hessian
                 shape      scale
    shape 9.157428e-05 0.02760638
    scale 2.760638e-02 8.57866385

                                                                 Empirical
                            Histogram                         #  Boxplot

     1.225+.                                                  1     |
          ......@  Theorectical                              18     |
          .........@....                                     53     |
          ..................@........... Empirical          113     |
          ...................................@              183  +-----+
          .......................................@.....     175  *--+--*
     0.925+..................................@              170  |     |
          ..................@........                       104  +-----+
          .........@...........                              77     |
          ...........                                        40     |
          ......@...                                         34     |
          ......                                             20     0
     0.625+..@                                               12     0
           ----+----+----+----+----+----+----+----+----+-
           * may represent up to 4 counts


                          Normal Probability Plot
      1.225+                                               +++*
           |                                           +++*****
           |                                       +*******
           |                                  *******
           |                            *******
           |                        *****+
      0.925+                   ******
           |                ****+
           |            +****
           |        ++***
           |    +++****
           |+++****
      0.625+***
            +----+----+----+----+----+----+----+----+----+----+
                -2        -1         0        +1        +2


    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utlfkil(d:/pdf/Weibull.pdf);
    %utlfkil(d:/txt/want.txt);

    %symdel alpha beta / nowarn;

    %let alpha=10;
    %let beta=1;

    %utl_submit_r64("
    library(fitdistrplus);
    library(actuar);
    library(haven);
    x <- rweibull(1000, &alpha, &beta);
    memp <- function(x, order) mean(x^order);
    weibul_mme <- mmedist(x, 'weibull', order = 1:2, memp=memp);
    fit.weibull<- fitdist(x, 'weibull', method = 'mme', order=c(1, 2), memp=memp, lower = c(0, 0));
    sink('d:/txt/want.txt');
    summary(fit.weibull);
    print(weibul_mme$hessian);
    sink();
    pdf(file='d:/pdf/Weibull.pdf');
    plot(fit.weibull, demp=TRUE);
    ");


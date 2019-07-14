---
authors:
- admin
categories: []
date: "2017-09-01T00:00:00Z"
draft: false
featured: false
gallery_item:
- album: gallery
  caption: Ocean
  image: theme-ocean.png
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)'
  focal_point: ""
  placement: 2
  preview_only: false
#lastmod: "2019-04-17T00:00:00Z"
projects: []
#subtitle: ''
summary: A Short Glance at the Gibbs Sampler.
tags:
- Softwares, Economics
title: 'A Basic Gibbs Sampler'
---


`Gibbs Sampler`, which is a specific case of `MH algorithm`, allows us to come up with values of ($\beta$, $\Sigma$) from joint distributions. Assuming that we have starting values for $\beta$ and $\Sigma$, and call them  $\beta^0$ and $\Sigma^0$. With those we will sample from the density of one element of parameter vector, conditional on the value of the other element sampled in the previous iteration. Thus the sampler will follow a recursive procedure. At the end we need to remove the effects of initial draws, which we call `burn-in` period. Lets take a bivariate example for Normal Distribution for which say we have $X$ is distributed as $N(0, \Sigma)$ and $\rho$ stands for the cross correlation between $x_1$ and $x_2$. The following code of [Julia Language](https://julialang.org/) will mimic this recursive procedure.


```julia
using Distributions
using DataFrames
using KernelDensity
using KernelEstimator
using StatsPlots
using Plots
gr()
```


```julia
rho = 0.45; # correlation
burn = 500; # burn in period
n = 500; # sample period

t = n+burn;
```


```julia
x1 = Array{Float64,2}(undef, t,1) 
x2 = Array{Float64,2}(undef, t,1);
```


```julia
fill!(x1, NaN)
fill!(x2, NaN);
```


```julia
x1[1] = 0 # initialise
x2[1] = 0 # initialise
```




    0




```julia
for i = 2:t
    x1[i] = rand(Normal(rho*x2[i-1],1-rho^2))
    x2[i] = rand(Normal(rho*x1[i-1],1-rho^2))
end
```


```julia
x1_new = x1[burn+1:end]
x2_new = x2[burn+1:end];
```


```julia
pl1 = plot(x1_new, color =:magenta, label="New X1", xlabel = "Observations", ylabel = "Values")
pl2 = plot(x2_new, color =:orange, legend=:topright, label="New X2", xlabel = "Observations", ylabel="Values")

plot(pl1, pl2, layout = (2,1))
```

![](/img/2017_09_01_1.png)




```julia
# Testing
a=mean(x1_new);
b=std(x1_new);
tstat = (a-0)/b
```




    -0.02487701521244865




```julia
if -1.96<tstat && tstat<1.96
    println("Not able to reject the NULL that expected value of x1_new is 0 \n")
else
    println("Reject the Null")
end
```

    Not able to reject the NULL that expected value of x1_new is 0 
    



```julia
d1 = density(x1_new, label = "X1 New")
d2 = density(x2_new, label = "X2 New")

p1 = plot(d1, line=:orange, fill = (0, :orange), legend=:topleft)
p2 = plot(d2, line=:green, fill = (0, :green), legend=:topleft)
plot(p1, p2, layout = (1,2))
```


![](/img/2017_09_01_2.png)


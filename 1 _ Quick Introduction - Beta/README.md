
# Non-Linear Techniques 


The common sense, even when we learn at school, generaly bring us a linearity thinking, the dedution of cause and directly effect. A sum tend to be better, always more and a subtraction like worst, lose of something, it is minus than previous. In fact to consilidate an act we need to align our thoughts and focus in one action (or one variable for time to resolve an equation or problem) . Besides linear intuition, unconsciouness thinking brings us a chaos of abstract process that we take time to learn and absorb as a real advantage. 
The most systems in real world respects a non-linear dynamics. Linear 
analysis techniques are currently in use (e.g., correlation, similarity) fail to detect 
features and complexities in nonlinearities regimes. 
Non-linear systems are part of complex systems. A large area of knowledge dealing with emerging behaviors:

![link](https://upload.wikimedia.org/wikipedia/commons/thumb/d/de/Complex_systems_organizational_map.jpg/1024px-Complex_systems_organizational_map.jpg)

Figure extracted from [5].

Systems with complexity are sometimes counter intuitive, have unexpected results and non-trivial behavior.


## Chaos

Chaos are an type of system considered in nonlinear techniques. They have simple periodic behavior to an unpredictable and  divergent regime. Linear systems are previsible, but in chaos pertubations generate huge differences along the predict outcomes. Whenever errors in linear process grows proportionally with predicted values, in chaos it considered desproportionately changes. 

The following example represent a way to identify an chaotic system: 

### Example for demonstration: Logistic Equation

Logic behavior (or equation): 

![gif](eq1.gif)

If look for graphical behavior varying values of 'x' variable ('quantities, like evolution of time'), we notice it converge to single state (Y axis is 0.6): 


```matlab
%Behavior converge to single state.

%%Script name: logistic_equation

x= rand; %initial value
a= 2.5;    % decision-maker parameter



for i=2:100  %loop to create logistic equation

x(i)= a*x(i-1)*(1-x(i-1));   %Logistic equation 

end

plot (x);
```

    
    


![png](output_6_1.png)


Changing the parameter, 'a' ('condition amount, or situation') before 2.5 and now to 3.24, the same equation has behaviour between two states (Y assumes two states 0.8 and 0.5):  


```matlab
%Changing the parameter has behaviour between two states.

%%Script name: logistic_equation



x= rand; %initial value
a= 3.24;    % decision-maker parameter



for i=2:100  %loop to creat logistic equation

x(i)= a*x(i-1)*(1-x(i-1));   %Logistic equation 

end

plot (x);
```

    
    


![png](output_8_1.png)


Changing more the parameter, now 'a' assume 4 of value, the system became chatioc:



```matlab
%Changing more the parameter the system became chatioc

%%Script name: logistic_equation



x= rand; %initial value
a= 4;    % decision-maker parameter (bifurcation parameter)



for i=2:100  %loop to creat logistic equation

x(i)= a*x(i-1)*(1-x(i-1));   %Logistic equation 

end

plot (x);
```

    
    


![png](output_10_1.png)


### Chaotic map: Feigenbaum Diagram

This map is a bifurcation diagram. It represents the chaotic evolution of any equation (or logic behaviour) :


```matlab

%Script extrated from [1]: https://booksite.elsevier.com/9780123708670/?ISBN=9780123708670
% pr17_1.m

% Feigenbaum Diagram



clear;

xn=0.01;
figure; 
hold;
for a=2.5:.02:4;                % range for coefficient a
    for k=1:.1:200              % iterate for 200 steps
        xn=a*xn*(1-xn);         % logistic equation
         if (k>100)             % Do not show initial values <100
            plot(a,xn,'k.');    % Plot the data points
        end;
    end;
end;

liney = [0:0.1:1];  % plot for red line
linex =  ones(size(liney,2))*3.569;

xlabel('a')                     % Provide labels and title
ylabel('state')
title('Feigenbaum Diagram Logistic Equation')
hold on 

plot(linex,liney,'r');

```

    Current plot held
    
    


![png](output_12_1.png)


Feigenbaum Diagram shows the state evolution of a system according the changes in parameter " a ". One moment it had one state, a=2.5, after two a~3.4 and the red line is the maker when the system (logic equation) became chatioc. 


### Linear X Non-Linear detection


The following graphic is possible to see a little of the limits of linear analyses. Considerer three systems, one linear, one random and another chaotic. In any analysis, random behaviour is not good to predict something, the results there isn't something like has patterns characteristics, they just respond randomly like truth dices. 


```matlab

%Scripts extrated from [1]: https://booksite.elsevier.com/9780123708670/?ISBN=9780123708670

% pr17_3.m
% Linear Time Series
clear;
% Measurement Function and Initial x value
p=0.8;
x1(1)=.1;
for n=2:1000
    x1(n)=p*x1(n-1)+randn(1); % Note the Dynamic Noise Term
end
% Plot Timeseries
figure;
subplot(3,3,1)
plot(x1)
title('Linear Timeseries')
% Autocorrelation
tt=-(length(x1)-1):length(x1)-1;
x1COV=xcov(x1,'coeff');

subplot(3,3,2)
plot(tt,x1COV,'k');
axis([-12 12 0 1]);
title('Autocorrelation ');
% Return Plot
for i=2:length(x1);
    subplot(3,3,3)
    plot(x1(i-1),x1(i),'k.');
    hold on
    
end;
title('Return Plot ');   



% pr17_4.m
% Nonlinear Time Series
clear;
% Measurement Function and Initial x value
p=4.0;
x2(1)=0.35;
for n=2:1000
    x2(n)=p*x2(n-1)*(1-x2(n-1)); % No Dynamic Noise Term
end
% Plot Timeseries
subplot(3,3,4)
plot(x2)
title('Nonlinear Timeseries')
% Autocorrelation
tt=-(length(x2)-1):length(x2)-1;
x2COV=xcov(x2,'coeff');

subplot(3,3,5)
plot(tt,x2COV,'k');
axis([-12 12 0 1]);
title('Autocorrelation ');
% Return Plot

for i=2:length(x2);
    subplot(3,3,6)
    plot(x2(i-1),x2(i),'k.');
    hold on
   
end;
title('Return Plot ');   


% pr17_5.m
% Random Time Series
clear;
x3=randn(1,1000);
% Plot Timeseries
subplot(3,3,7)
plot(x3)
title('Random Timeseries')
% Autocorrelation
tt=-(length(x3)-1):length(x3)-1;
x3COV=xcov(x3,'coeff');
subplot(3,3,8)
plot(tt,x3COV,'k');
axis([-12 12 0 1]);
title('Autocorrelation ');
% Return Plot

for i=2:length(x3);
    subplot(3,3,9)
    plot(x3(i-1),x3(i),'k.');
    hold on
    
end;
title('Return Plot');   
```

    
    


![png](output_14_1.png)


The first column are the three systems, in the second column are on type of linear analysis (Autocorrelation) and the third column one type of nonlinear analysis (Return plot). In the second column the autocorrelation fail to detect diferences between Nonlinear and Random timeseries, otherwise return plot detect differents behaviors for the three systems . 

### Attractors 

Improving the nonlinear tools lead to discoveries that chaotics, fractals regimes, for example,  respects cycles of patterns that envolve in multidimensional environment. 

Usually it is common analyze variables in two dimensional graphic ('Y' in function of 'X', y(x) or f(x) ), but to understand complex systems is necessary go beyond two dimensional behaviors, which the empower about information be more transparent to human analysis what is going on in the system . This context culminates in other set of analyses, the attractors.

In few words and first contact, attractors are a set of invariant states repecting severeal dynamics while envolve in multidimentional phase space.

The two figures below are examples of logistic equation if construct the attractor :

![png](at1.png)

Figure extracted from [3]. Show the attractor of logistic equation.

![png](at2.png)

Figure extracted from [3]. Show the attractor of logistic equation in blue points and red points are what happen when try to construct attractors from random information.


The logistic attractor has few dimensions, but attractors can envolve more than three dimensions like strange attractors:

![jpg](satt.jpg)

Figure of strang attractor, extracted from [4].

One famous attractor is butterfly effect (Lorenz's strange attractor): 

![png](be.png)

Figure extracted from [5].


### Conclusions

The science of non-linearity is whole new universe of tools to measure, validate and understand the behavior of nature. The mathematical logic behind helps to look and think different about the problems and how you can solve them. 



## References

1. Signal Processing for Neuroscientists, Wim Drongelen, 2006.

2. Nonlinear Dynamics and Chaos: With applications to physics, biology, chemistry, and engineering, Steven H. Strogatz, 1994. 

3. Visual Analysis of Nonlinear Dynamical Systems: Chaos, Fractals, Self-Similarity and the Limits of Prediction, Geoff Boeing, 2016.

4. Attractors rendered by David A. Ferreira, CGMK, disponível em: https://www.cgmonkeyking.com/projects/m05Jy.

5. Wikipedia.



```matlab

```

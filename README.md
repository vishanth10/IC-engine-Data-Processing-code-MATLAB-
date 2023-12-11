# IC-engine-Data-Processing-code-MATLAB-

Developed by VHR at IIT Madras for IC Engine Laboratory for Data Analysis, visualisation and predicions of abnormalities for testing engine with variable parameters

MATLAB Code
-Code for data processing  and graph plotting from raw data imported from measuring instrument.


Sample Code:

numdata10 = xlsread('crankpressure100.xlsx');
% this for injection pressure which 100 bar plot against crank angle and cylinder pressure%
crankobserved = reshape(crankangle,7200,111);
pressureobserved = reshape(pressure,7200,111);
pressure = pressure(:);
M = max(pressure);
[maxNum, maxIndex] = max(pressureobserved(:)); %finding max pressure of each cycle
[row, col] = ind2sub(size(pressureobserved), maxIndex); %finding corresponding crankangle data of the cycle%
Maxpressure = max(pressureobserved); %finding total max pressure of all cycles%
for i= [1:111]
    for j= [1:7200]
        for k =[1:111]
     if (pressureobserved(j,i)==Maxpressure(1,k))   %find the CA data for high max pressure of all the cycle%
         m(1,k) = crankobserved(j,i);
      
     end
        end
     end
       
end
 
[minNum, minIndex] = min(Maxpressure(:)); %finding minimum of max pressure of total cycle
[row1, col1] = ind2sub(size(Maxpressure), minIndex); %finding corrosponding crank angle of all cycles%
minipressurecycleplotCA = crankobserved(:,[col1]);
minipressureplotP = (:,[col1]);
x = crankobserved(:,[col]);
y = pressureobserved(:,[col]);
%new type loop instead of ifelse%
t1 = simCA;  %simulated CA data
[row,column] = size(t1); %find the size of the data 
[n,r] = quorem(row,sym(720));  % find the no of cycles%
for e = [1:row]         % loop is for reducing the crank angle to its -360 to 360 range in simulation%
    for im = [0:n+1]
if ((t1(e,1))>360+(720*im)&&(t1(e,1))<((360+(720*im))+720))
    t1(e,1)= t1(e,1)-(720+(720*im));
end
     end
end
%end%
for e = [1:row]
    y0(e,1)=10*simpressure(e,1); %simulated pressure data is multipled by 10 for unit conversions
end
for i= row:((n+1)*720)   %equating the pressure data for the plotting%
    x0(i,1)=NaN;
    y0(i,1)=NaN;
end
 
simulatedCA = reshape(x0,720,n+1);
tsimulatedPA = reshape(y0,720,n+1);
 
plot (x,y)
hold on 
plot (minipressurecycleplotCA,highpressureplotP)
scatter (m,Maxpressure)
plot(simulatedCA,tsimulatedPA)
 
hold off

 
 


![image](https://github.com/vishanth10/IC-engine-Data-Processing-code-MATLAB-/assets/38405533/e914ac8b-866e-4259-ac33-289ace3de5cc)

# Matlab
clear all
global key
screen=zeros(20,10);
flow=zeros(20,10);
stack=zeros(20,10);
scrreset=zeros(20,10);
% figure
figure('keypressfcn',@aaa)
for i=1:10000
newpiece=randi(7);
% newpiece=2;
flow=zeros(20,10);
switch newpiece
    case 1       
        flow(end,5)=newpiece;
        flow(end,6)=newpiece;
        flow(end-1,6)=newpiece;
        flow(end-2,6)=newpiece;
    case 2       
        flow(end,6)=newpiece;
        flow(end-1,6)=newpiece;
        flow(end-2,6)=newpiece;
        flow(end-3,6)=newpiece;
    case 3               
        flow(end,5)=newpiece;
        flow(end,6)=newpiece;
        flow(end-1,5)=newpiece;
        flow(end-1,6)=newpiece;
   case 4       
        flow(end,6)=newpiece;
        flow(end-1,5)=newpiece;
        flow(end-1,6)=newpiece;
        flow(end-1,7)=newpiece;
   case 5       
        flow(end,6)=newpiece;
        flow(end-1,5)=newpiece;
        flow(end-2,5)=newpiece;
        flow(end,5)=newpiece;
   case 6       
        flow(end,5)=newpiece;
        flow(end,6)=newpiece;
        flow(end-1,6)=newpiece;
        flow(end-1,7)=newpiece;
   case 7      
        flow(end,6)=newpiece;
        flow(end,7)=newpiece;
        flow(end-1,5)=newpiece;
        flow(end-1,6)=newpiece;            
   end


% stack(1,:)=2;
sumsA=sum(sum(stack~=0));
screen=stack+flow;
sumsB=sum(sum(screen~=0));
if sumsA~=sumsB-4
    break
end

snum_1=sum(sum(screen~=0));
flowA=flow;
flowB=flow;

for jj=1:1000
%     pause(.1);
% x=input('in');
pause(.1)
% op=xlsread('operating.xlsx','A1:A1');

if strcmpi(key,'e')
 flowB=[flowB(:,2:end),zeros(20,1)];
 key=' ';
 %%%如果顶到左右边界？
end
if strcmpi(key,'r')
 flowB=[zeros(20,1),flowB(:,1:end-1)];
 key=' ';
 %%%如果顶到左右边界？
end
flowB=[flowB(2:end,:);zeros(1,10)];
% flowB=[flowA(:,2:end),zeros(20,1)];
screen=stack+flowB;
snum_2=sum(sum(screen~=0));
if snum_2~=snum_1
    flowB=flowA;
    screen=stack+flowB;
    stack=screen;
    prfsc(screen);
    
diss=(scrreset~=screen)';
disrow=sum(diss);
if ~isempty(find(disrow==9,1))
    fullrowid=find(disrow==9);
    screen(fullrowid,:)=[];
    stack=[screen;zeros(length(fullrowid),10)];
    prfsc(stack);
end
    break
end
screen=stack+flowB;
 prfsc(screen);
flowA=flowB;
end

end

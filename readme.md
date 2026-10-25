# Optimization Algorithm for Inventory Control Problem Based on Weevil Worm Damage (Matlab Code Implementation)

​  
Editor
Then this paper solves the TSP problem based on the optimizing algorithm of ant damage, and realizes it with Matlab code.
📚2 Running Results Edit
Editor
Part of the code:
%% Problem Definition  
model=CreateModel2();            % Create Model  
model.Umax=400;  
CostFunction=@(xhat) MyCost(xhat,model);   % Cost Function  
VarSize=[model.K model.H]; % Size of Decision Variables Matrix  
nVar=prod(VarSize);  % Number of Decision Variables  
VarMin=0;    % Lower Bound of Variables  
VarMax=1;    % Upper Bound of Variables  
%% WDOA Parameters  
MaxIt = 200;     % Maximum Number of Iterations  
nPop = 400;      % Number of weevils  
DamageRate = 0.1;         % Damage Rate  
nweevil = round(DamageRate*nPop); % Number of Remained weevils  
nNew = nPop-nweevil;        % Number of New weevils  
mu = linspace(1, 0, nPop);     % Mutation Rates  
pMutation = 0.2;          % Mutation Probability  
MUtwo = 1-mu;           % Second Mutation  
SnoutPower = 0.8;         % Weevil Snout power Rate  
FlyPower = 0.03*(VarMax-VarMin);  % Weevil Fly Power Rate  
%% Basics  
% Empty weevil  
weevil.Position = [];  
weevil.Cost = [];  
weevil.Sol = [];  
% Weevils Array  
pop = repmat(weevil, nPop, 1);  
% First weevils  
for i = 1:nPop  
pop(i).Position = unifrnd(VarMin, VarMax, VarSize);  
[pop(i).Cost pop(i).Sol] = CostFunction(pop(i).Position);  
end;  
% Sort  
[~, SortOrder] = sort([pop.Cost]);pop = pop(SortOrder);  
% Best Solution  
BestSol = pop(1);  
% Best Costs Array  
BestCost = zeros(MaxIt, 1);  
%--------------------------------  
%% WDOA Body  
for it = 1:MaxIt  
newpop = pop;  
for i = 1:nPop  
for k = 1:nVar  
if rand <= MUtwo(i)  
TMP = mu;TMP(i) = 0;TMP = TMP/sum(TMP);  
j = RouletteWheelS(TMP);  
newpop(i).Position(k) = pop(i).Position(k)+SnoutPower*(pop(j).Position(k)-pop(i).Position(k));  
end;  
% Mutation  
if rand <= pMutation  
newpop(i).Position(k) = newpop(i).Position(k)+FlyPower*randn;  
end;end;  
% Apply Lower and Upper Bound Limits  
newpop(i).Position = max(newpop(i).Position, VarMin);  
newpop(i).Position = min(newpop(i).Position, VarMax);  
[newpop(i).Cost newpop(i).Sol] = CostFunction(newpop(i).Position);  
end;% Asses power  
[~, SortOrder] = sort([newpop.Cost]);newpop = newpop(SortOrder);% Sort  
pop = [pop(1:nweevil);newpop(1:nNew)];% Select  
[~, SortOrder] = sort([pop.Cost]);pop = pop(SortOrder);% Sort  
BestSol = pop(1);% Update  
BestCost(it) = BestSol.Cost;% Store  
if BestSol.Sol.IsFeasible  
Flag=' *';  
else  
Flag='';  
end  
% Iteration  
disp(['Iteration ' num2str(it) ': WDOA Best Cost = ' num2str(BestCost(it)) Flag]);  
% Plot Solution  
figure(1);  
PlotSolution(BestSol.Sol,model);  
end  
%% ITR  
figure;  
plot(BestCost,'k', 'LineWidth', 2);  
xlabel('ITR');  
ylabel('Cost Value');  
ax = gca;  
ax.FontSize = 14;  
ax.FontWeight='bold';  
set(gca,'Color','c')  
grid on;  
%%  
BestSol.Sol  
disp(['Sum of Orders or Products Costs ' num2str(BestSol.Sol.SumAX)]);  
disp(['Sum of Inventory or Maintenance Costs ' num2str(BestSol.Sol.SumBI)]);  
disp(['Used Capacity ' num2str(BestSol.Sol.UC)]);  
🎉3 References
🌈4 Matlab code and article reading

## Images

![Optimization algorithm for inventory control problem based on ant damage optimization (Matlab code implementation)](01.png)
![Optimization algorithm for inventory control problem based on ant damage optimization (Matlab code implementation)](02.png)
![Optimization algorithm for inventory control problem based on ant damage optimization (Matlab code implementation)](03.png)
![Optimization algorithm for inventory control problem based on ant damage optimization (Matlab code implementation)](04.png)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->

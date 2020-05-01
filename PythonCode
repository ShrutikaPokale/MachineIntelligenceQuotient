print("Enter Tau (values separated by space)")
Tau=input().split(" ")
print("Enter interface complexity cmh,chm")
comp=input().split(",")
complex={}
complex["cmh"]=comp[0]
complex["chm"]=comp[1]
print("Enter the dimension of data transfer matrix F in format x,y")
F=input().split(",")
print(F)
FM={}
AM={}

'setting the values of Data transfer matrix to zero'
for i in range(1,int(F[0])+1):      
    for j in range(1,int(F[0])+1):
        c1=str(i)+str(j)
        FM[c1]=0
        
'setting the values of Task Allocation matrix to zero'
for x in range(1,int(F[0])+1):      
    for y in range(1,4):
        c2=str(x)+str(y)
        AM[c2]=0   

'if value entered is not as per requirement'
def change_value(value):
    for i in range(len(value)):     
        for j in range(3):
            k=value[i][j][1:]
            print("Enter the value of A"+k)
            v=int(input())
            AM[k]=v
    check()

'to check whether the value entered is correct or not'                                    
def check():                    
    wrong=[]
    for m in range(1,int(F[0])+1):
        w=[]
        A_sum=0
        for n in range(1,4):
            c=str(m)+str(n)
            w.append("A"+c)
            A_sum+=int(AM[c])
        if A_sum>1:
            wrong.append(w)
    if len(wrong)!=0:
        print(wrong,"Change the values accordingly as sum of values in each group must be equal to 1")
        change_value(wrong)

'to enter values in matrix F and A'
def F_A():                  
    count=0
    while(count==0):
        print("To enter the values in Data Transfer Matrix F? FY or Task Allocation Matrix a? AY or exit? EXIT")
        response=input()
        if response.upper()=="FY":
            print("Enter in format Fij=val")
            entry=input()
            if entry[0]=='F'and 1<=int(entry[1])<=int(F[0]) and 1<=int(entry[2])<=int(F[0]) and entry[3]=="=" and entry[4:].isdigit():
                FM[entry[1:3]]=entry[4:]
            else:
                print("Entered values are not in required format")
                F_A()
        elif response.upper()=="AY":
            print("Enter in format Aij=val")
            entry=input()
            if entry[0]=='A'and 1<=int(entry[1])<=int(F[0]) and 1<=int(entry[2])<=3 and entry[3]=="=" and int(entry[4]) in [0,1]:
                AM[entry[1:3]]=entry[4]
            else:
                print("Entered values are not in required format")
                F_A()
        elif response.upper()=="EXIT":
            break
    check()

F_A()

'Calculate CIQ'
def CIQ():                  
    sum1=0
    sum2=0
    for key,value in AM.items():
        if key[-1]=="1":
            sum1+=(int(value)*int(Tau[int(key[-2])-1]))
        elif  key[-1]=="2":
            sum2+=(int(value)*int(Tau[int(key[-2])-1]))
           
    print("CIQ=",sum1+sum2)
    return(sum1+sum2)

'Calculate HIQ'
def HIQ():                   
    sum1=0
    sum2=0
    sum3=0
    AM_keys=AM.keys()
    AM_val=AM.values()
    for key,value in AM.items():
        if key[-1]=='2':
            sum1+=(int(value)*int(Tau[int(key[-2])-1]))
    key1=[]
    key2=[]       
    for keys in AM_keys:
        if keys[-1]=="1": 
            key1.append(keys)
        elif keys[-1]=='2':
            key2.append(keys)
    for k1 in key1:
        for k2 in key2:
            ind1=k1[0]
            ind2=k2[0]
            sum2+=(int(AM[k1])*int(AM[k2])*int(FM[ind1+ind2]))
            sum3+=(int(AM[k1])*int(AM[k2])*int(FM[ind2+ind1]))
    HIQ=sum1+float(complex['cmh'])*sum2+float(complex['chm'])*sum3 
    print("HIQ=",HIQ) 
    return(HIQ)
   
print("Tau=",Tau)
print("Interface Complexity=",complex)
print("Data Transfer Matrix F=",FM)
print("Task Allocation Matrix A=",AM)
CIQ=CIQ()
HIQ=HIQ()
MIQ=CIQ-HIQ
print("MIQ=",MIQ)

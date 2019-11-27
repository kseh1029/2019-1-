Term Project 1.
Exploitation vs Exploration in the Huffman Encoding

Ⅰ. 프로젝트 결과

Ⅱ. 프로젝트 목적, 접근방법 및 세부결과
확률을 모르는 임의로 배치된 알파벳의 집합이 있는 텍스트 문서에서 Data Compression 중 Huffman Encoding 을 이용하여 적절한 확률을 구하여 데이터에 비트를 부여할때와, 이미 주어진 ASCII를 이용하여 각각 7비트를 부여할 때 어떠한 경우가 비트수를 절약하여 더 나은 압축효과를 얻을 수 있는지를 확인하는 프로젝트이다.

처음 텍스트 문서를 불러왔을 때, 알파벳이 임의로 배치되어 있고 알파벳 각각의 확률을 모르므로 바로 Huffman Encoding을 할 수 없다. 따라서 적당한 개수의 알파벳을 ASCII 로 읽으면서 확률을 구하고 Huffman Encoding을 진행한다. 그리고, 나머지 알파벳을 확률에 따라 Huffman Encoding에서 구한 비트를 부여하면 된다

30000개 7bits ASCII
나머지 Huffman Encoding 일 때
실제로 MATLAB을 이용하여 코드를 짜본결과,
전체 배열을 7bits ASCII
 전체 배열을 7bits ASCII 로 부여하게 되면, 평균 Code Length 는 7이 나오게 되며
30000개는 7bits ASCII 로 부여하면서 적절한 확률을 얻고, Huffman Encoding을 하여 비트를 부여하게 되면 평균 Code Length 는 3.755로 감소하는 것을 확인하였다.
본 보고서의 첫 번째 페이지에서 아스키코드가 7비트, 6비트, 4비트, 2000비트 일때의 상황을 가정하고 배열의 어느정도를 확률을 구하는데 사용하면 Code Length 가 가장 작은지를 확인해본 결과를 나타내었다. 7Bits ASCII 의 경우는 137 번째 까지 Exploration 하면
137 번째 까지 Exploration
 Optimal 한 Code Length를 얻을 수 있다. 실제로 30000 개를  Exploration 했을 때에는 평균 Code Length 가 3.755 이지만, 137 개를 Exploration 했을 때에는 평균 Code Length 가 2.3835 로 감소하여 같은 결과를 적은 Code Length 로 압축하여 표현할 수 있다.


Optimal 한 Huffman Bit
이때의 호프만 비트는 아래 사진처럼 부여되어있으며, 이 비트수를 이용하여 Kraft Inequality를 구해본 결과 (작업공간 내 Check 배열) 1이 나오는 것을 확인할 수 있었다.
가장 Optimal 한 경우는 7bits 에서는 134개나 135개를 사용했을때이다.
이때의 평균 Code length 는 2.3834로 서로 동일하다.
Ⅲ. 프로젝트 코드 및 해석
% 2017117876 // Term Project 1
clc; close all; clear; % 충돌을 막기위한 과거값 삭제
 
f_id = fopen('source_JPARK2019_vfinal.txt', 'r');
format_read = '%2s';
Original_Array = fscanf(f_id,format_read);
size = length(Original_Array);
for destination=1:1:500
Count_ASCII=[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]; % Count_ASCII 는 sum 을 하므로 0으로 초기화
Count_Huffman=[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0]; % Count_Huffman 은 sum 을 하므로 0으로 초기화
 
% 아래 for 문에서 A~Z 까지 Probability 계산에 사용할 Array Scanning
for i=1:1:destination
 if Original_Array(1,i) == 'a'
     Count_ASCII(1,1) = Count_ASCII(1,1) + 1;
     continue
 end
 if Original_Array(1,i) == 'b'
     Count_ASCII(1,2) = Count_ASCII(1,2) + 1;
     continue
 end
 if Original_Array(1,i) == 'c'
     Count_ASCII(1,3) = Count_ASCII(1,3) + 1;
     continue
 end
  if Original_Array(1,i) == 'd'
     Count_ASCII(1,4) = Count_ASCII(1,4) + 1;
     continue
 end
 if Original_Array(1,i) == 'e'
     Count_ASCII(1,5) = Count_ASCII(1,5) + 1;
     continue
 end
 if Original_Array(1,i) == 'f'
     Count_ASCII(1,6) = Count_ASCII(1,6) + 1;
     continue
 end
 if Original_Array(1,i) == 'g'
     Count_ASCII(1,7) = Count_ASCII(1,7) + 1;
     continue
 end
  if Original_Array(1,i) == 'h'
     Count_ASCII(1,8) = Count_ASCII(1,8) + 1;
     continue
 end
 if Original_Array(1,i) == 'i'
     Count_ASCII(1,9) = Count_ASCII(1,9) + 1;
     continue
 end
 if Original_Array(1,i) == 'j'
     Count_ASCII(1,10) = Count_ASCII(1,10) + 1;
     continue
 end
 if Original_Array(1,i) == 'k'
     Count_ASCII(1,11) = Count_ASCII(1,11) + 1;
     continue
 end
  if Original_Array(1,i) == 'l'
     Count_ASCII(1,12) = Count_ASCII(1,12) + 1;
     continue
 end
 if Original_Array(1,i) == 'm'
     Count_ASCII(1,13) = Count_ASCII(1,13) + 1;
     continue
 end
 if Original_Array(1,i) == 'n'
     Count_ASCII(1,14) = Count_ASCII(1,14) + 1;
     continue
 end
 if Original_Array(1,i) == 'o'
     Count_ASCII(1,15) = Count_ASCII(1,15) + 1;
     continue
 end
  if Original_Array(1,i) == 'p'
     Count_ASCII(1,16) = Count_ASCII(1,16) + 1;
     continue
 end
 if Original_Array(1,i) == 'q'
     Count_ASCII(1,17) = Count_ASCII(1,17) + 1;
     continue
 end
 if Original_Array(1,i) == 'r'
     Count_ASCII(1,18) = Count_ASCII(1,18) + 1;
     continue
 end
 if Original_Array(1,i) == 's'
     Count_ASCII(1,19) = Count_ASCII(1,19) + 1;
     continue
 end
  if Original_Array(1,i) == 't'
     Count_ASCII(1,20) = Count_ASCII(1,20) + 1;
     continue
 end
 if Original_Array(1,i) == 'u'
     Count_ASCII(1,21) = Count_ASCII(1,21) + 1;
     continue
 end
 if Original_Array(1,i) == 'v'
     Count_ASCII(1,22) = Count_ASCII(1,22) + 1;
     continue
 end
 if Original_Array(1,i) == 'w'
     Count_ASCII(1,23) = Count_ASCII(1,23) + 1;
     continue
 end
  if Original_Array(1,i) == 'x'
     Count_ASCII(1,24) = Count_ASCII(1,24) + 1;
     continue
 end
 if Original_Array(1,i) == 'y'
     Count_ASCII(1,25) = Count_ASCII(1,25) + 1;
     continue
 end
 if Original_Array(1,i) == 'z'
     Count_ASCII(1,26) = Count_ASCII(1,26) + 1;
     continue
 end
 
end
 
% 아래 for 문에서 평균을 구하기 위한 정확한 length 파악 (a~z 만 허용)
sum=0;
for i=1:1:26
sum = sum + Count_ASCII(1,i);
end
 
% 아래 for 문에서 a~z 까지 나올 Probability 를 계산
for i=1:1:26
prob(1,i)=Count_ASCII(1,i)/sum;
end
for i=1:1:26
    if i==1
    prop_accumulation(1,i) = prob(1,i);
    else
    prop_accumulation(1,i) = prop_accumulation(1,i-1) + prob(1,i);
    end
end
 
 
% MATLAB Add-on 중 Communications Toolbox 에 있는 huffmandict 을 사용
symbols = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26];
huffman_bit = huffmandict(symbols,prob);
 
% huffman coding 된 Array의 length 를 파악
for i=1:1:26
huffman_length(1,i)=length(huffman_bit{i,2});
end
 
% huffman coding 이 제대로 됐는지 확인하기 위해 Kraft Inequality = 1 만족임을 Check.
check = 0;
for i=1:1:26
check = check + (1/2)^(huffman_length(1,i));
end
 
% 아래 for 문에서 A~Z 까지 Huffman 에 사용할 Array Scanning
for i=destination+1:1:size
 if Original_Array(1,i) == 'a'
     Count_Huffman(1,1) = Count_Huffman(1,1) + 1;
     continue
 end
 if Original_Array(1,i) == 'b'
     Count_Huffman(1,2) = Count_Huffman(1,2) + 1;
     continue
 end
 if Original_Array(1,i) == 'c'
     Count_Huffman(1,3) = Count_Huffman(1,3) + 1;
     continue
 end
  if Original_Array(1,i) == 'd'
     Count_Huffman(1,4) = Count_Huffman(1,4) + 1;
     continue
 end
 if Original_Array(1,i) == 'e'
     Count_Huffman(1,5) = Count_Huffman(1,5) + 1;
     continue
 end
 if Original_Array(1,i) == 'f'
     Count_Huffman(1,6) = Count_Huffman(1,6) + 1;
     continue
 end
 if Original_Array(1,i) == 'g'
     Count_Huffman(1,7) = Count_Huffman(1,7) + 1;
     continue
 end
  if Original_Array(1,i) == 'h'
     Count_Huffman(1,8) = Count_Huffman(1,8) + 1;
     continue
 end
 if Original_Array(1,i) == 'i'
     Count_Huffman(1,9) = Count_Huffman(1,9) + 1;
     continue
 end
 if Original_Array(1,i) == 'j'
     Count_Huffman(1,10) = Count_Huffman(1,10) + 1;
     continue
 end
 if Original_Array(1,i) == 'k'
     Count_Huffman(1,11) = Count_Huffman(1,11) + 1;
     continue
 end
  if Original_Array(1,i) == 'l'
     Count_Huffman(1,12) = Count_Huffman(1,12) + 1;
     continue
 end
 if Original_Array(1,i) == 'm'
     Count_Huffman(1,13) = Count_Huffman(1,13) + 1;
     continue
 end
 if Original_Array(1,i) == 'n'
     Count_Huffman(1,14) = Count_Huffman(1,14) + 1;
     continue
 end
 if Original_Array(1,i) == 'o'
     Count_Huffman(1,15) = Count_Huffman(1,15) + 1;
     continue
 end
  if Original_Array(1,i) == 'p'
     Count_Huffman(1,16) = Count_Huffman(1,16) + 1;
     continue
 end
 if Original_Array(1,i) == 'q'
     Count_Huffman(1,17) = Count_Huffman(1,17) + 1;
     continue
 end
 if Original_Array(1,i) == 'r'
     Count_Huffman(1,18) = Count_Huffman(1,18) + 1;
     continue
 end
 if Original_Array(1,i) == 's'
     Count_Huffman(1,19) = Count_Huffman(1,19) + 1;
     continue
 end
  if Original_Array(1,i) == 't'
     Count_Huffman(1,20) = Count_Huffman(1,20) + 1;
     continue
 end
 if Original_Array(1,i) == 'u'
     Count_Huffman(1,21) = Count_Huffman(1,21) + 1;
     continue
 end
 if Original_Array(1,i) == 'v'
     Count_Huffman(1,22) = Count_Huffman(1,22) + 1;
     continue
 end
 if Original_Array(1,i) == 'w'
     Count_Huffman(1,23) = Count_Huffman(1,23) + 1;
     continue
 end
  if Original_Array(1,i) == 'x'
     Count_Huffman(1,24) = Count_Huffman(1,24) + 1;
     continue
 end
 if Original_Array(1,i) == 'y'
     Count_Huffman(1,25) = Count_Huffman(1,25) + 1;
     continue
 end
 if Original_Array(1,i) == 'z'
     Count_Huffman(1,26) = Count_Huffman(1,26) + 1;
     continue
 end
 
end
 
% huffman coding 된 code length 파악
huffman_code_length = (huffman_length) .* (Count_Huffman);
huffman_code_length_sum=0;
for i=1:1:26
huffman_code_length_sum = huffman_code_length_sum + huffman_code_length(1,i);
end
 
% ASCII 의 code length 파악
ASCII_code_length = 7 * destination;
 
% total code length 파악
Total_code_length = ASCII_code_length + huffman_code_length_sum;
 
% average code length 파악
Average_code_length = Total_code_length/size;
 
result(1,destination) = Average_code_length;
end
 
% 사용되는 평균 code length plot
x=1:1:500;
figure();
bar(x,result,'b');
xlabel 'ASCII Exploreration Count'
ylabel 'Average Code Length'
title 'when ASCII 7 bits'
grid on;

Ⅳ. 고찰
예상했던 대로, 단순히 exploitation 하는 것 보다, exploration을 하면서 그 순간의 이득은 포기하면서도, Huffman Encoding을 하는 것이 더욱더 효율적이며 데이터 압축효과가 좋았다. 다만, 코드를 작성하면서 간단한 경우에 대한 의문점을 가지게 되었다. Devide and Conqure을 이용하여 알고리즘을 해결하기 위해, 우선 간단한 [a,b,c,a,b,c,a,a] 라는 8개 배열을 이용하여 손으로 Huffman Encoding을 해 보았다. 이때 4개는 7 bits ASCII를 하며 확률을 구하고, 나머지 4개는 이때 구한 확률로 비트를 부여해봤는데 처음 4개는 a가 2개, b가 1개, c가 1개라서 각각 P(a) = 1/2, P(b) = 1/4, P(c) = 1/4 였으며 각각 0, 10, 11 이라는 비트를 부여하면 됐다. 결국 ASCII를 4개부여하므로 28비트, 나머지 4개는 a가 2개이므로 2비트, b가 1개이므로, 2비트, c가 1개이므로 2비트 이므로 34비트가 되며 평균 Code Length 는 34/8 로 4.25가 나올것이라고 예상했다.
 하지만 코드로 구현을 해 본 결과, 4.3750이 나왔다. 그래서 확인해보니 Huffman_code_length_sum 이 6이 나와야하는데 7이 나온 것을 알게 되었고
 a와 c 는 손으로 계산했을때와 마찬가지로 0 과 10 이 나왔는데 b는 P(b) = P(c) 임에도 불구하고 110 이 나왔다.
이는 a~z 까지 모두 Huffman bit를 부여하면서, d~z 까지 엄청나게 긴 비트가 있어서 생긴 일 이였다. 그래서 a~c 까지만 비트를 부여
하도록 바꿔주니, 정상적으로 b와 c에 2자리의 비트가 주어졌다.
추가적으로 Prop_Accumulation 이라는 배열도 만들었는데, 이 배열은 각각의 알파벳이 나올 확률을 합산해가며 만든 배열이다. 즉 [P(a), P(a)+P(b), P(a)+P(b)+P(c), ] 로 구성되어있으며 rand 함수를 사용하여 0~1 사이의 랜덤한 값이 나왔을 때, 어떤 알파벳을 출력할지 결정하는 방법이 된다.

아래의 사진은 137번째 까지 7bits ASCII 로 Exploration 했을때의 Prop_Acc이다.
P(a) = 0.0219 이며, P(a) + P(b) = 0.0949 이므로,  일 때 a 이며,
 일 때 b 이다. 이와 같은 루틴으로  일 때 i 이므로, j~z 는 나오지 않음을 확인이 가능하다.
if 문 중첩하여 해당 구간일 때 해당 알파벳이 출력하는 방식으로 확률에 따른 알파벳을 출력시킬 수 있다.

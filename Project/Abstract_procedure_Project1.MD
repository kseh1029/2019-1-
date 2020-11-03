%--------------------------------------------------------------------------
% Code by Jeonghun Park, 2019 Apr.
% ITEC201006 : Introduction to Computer Science and Engineering Project
% Sample read
%--------------------------------------------------------------------------

clc; close all; clear;

f_id = fopen('source_JPARK2019_vfinal.txt', 'r');
format_read = '%2s';

Sample_r = fscanf(f_id,format_read);

OurSource = [];
SourceCount = [];

sample_length = length(Sample_r);

LearningPhase_array = 1000:1000:80000;

for idx_learning = 1:length(LearningPhase_array)
    LearningPhase = LearningPhase_array(idx_learning);
    
    for idx = 1:LearningPhase
        if ismember(Sample_r(idx), OurSource)
            sample_idx = find(Sample_r(idx) == OurSource);
        else
            OurSource = [OurSource, Sample_r(idx)];
        end
    end
    
    for idx = 1:length(OurSource)
        SourceCount(idx) = count(Sample_r(1:LearningPhase), (OurSource(idx)));
    end
    
    Prob = SourceCount/LearningPhase;
    
    %     -----------------
    %     Huffmand(Prob)
    %     -----------------
    
    %     -----------------
    %     Bit length (LearningPhase+1 ~ End) by using Huffman
    %     -----------------
    
    %     -----------------
    %     Total_bit = 6*LearningPhase + Huffman_bit_length
    %     Avg_bit(idx_learning) = Total_bit/10^5;
    %     -----------------
    
end

% plot(LearningPhase_array, Avg_bit)



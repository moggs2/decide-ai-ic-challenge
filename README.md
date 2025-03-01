# ICP AI Challenge Repo

## An overview what was changed and found for the challenge

### Installation and first steps

As the advanced challenge the first AI challenge was chosen. The task was to deploy a GPT2 model and analyse costs and answers of the model.

For starting out the decide-ai-ic repo was forked on GitHub.

Then the requirements were installed on a Debian 12 VPS like described in the repo.

One change was made because Rust was outdated:
"rustup target add wasm32-wasi" was changed to "rustup target add wasm32-wasip1". Any missing wasm packages which came up during installatin were installed as well. 
The dfx.json was changed accordingly and can be found in this repo.

The canister was started locally with "dfx start" and "dfx deploy". Different questions were checked for answers and cycles.

### Answers from GPT2 

After checking some questions different quality was seen. The answers were sometimes correct, sometimes wrong and sometimes got different answers after retrying. The grammar and spelling was correct usually. Moreover GPT2 understood the questions in general. For instance a question about what is the highest mountain in Europe GPT2 was answered with "Mount Everest, Himalaya". The question "what is the most popular coding language" was answered with "Java" and sometimes with "Python". Questions about the capital of different countries were answered correctly. The question what could be the healthiest popular food were answered sometimes with "joghurt" and sometimes with a "rice meal". The output length made the answer either more precise or descriptive. Sometimes the output length was too short because the sentence was not finished. But very often this was fixed by increasing the temperature. By increasing the temperature GPT2 went over to a list. For instance three very healthy foods (broccoli, sushi, chicken) were given and not a sentence like "Chicken is the healthiest popular food. It is ..."

## Tables

Table of cycles counted for different input and output length.

| Input Length | gen_1 | gen_2 | gen_4 | gen_8 |
|-------------|--------|--------|--------|--------|
| 1 | 214M | 291M | 465M | 813M |
| 2 | 228M | 315M | 487M | 834M |
| 4 | 328M | 415M | 589M | 935M |
| 8 | 389M | 471M | 644M | 992M |
| 16 | 597M | 673M | 847M | 1195M |
| 32 | 1156M | 1243M | 1418M | 1769M |
| 64 | 2383M | 2470M | 2648M | 3004M |

### General differences

The numbers found for this challenge are quite similiar. One main difference are the numbers in the first and the last column. The numbers in the first column are a bit higher than the comparison table of the fork. The last column contains a bit lower numbers.

### Incremental differences

The cost for additional tokens remained not stable for 3 additional tokens. There was an increase. But 1 additional tokens and 7 additional tokens remained stable with about 85M cycles.

   - Generating 1 additional token: ~83M cycles
   - Generating 3 additional tokens: ~258M cycles (129M per token)
   - Generating 7 additional tokens: ~607MM cycles (87M per token)

The localhost cannot execute more than 4B cycles. Therefore the input length of 128 was not possible.

The table of instructions from the forked repo to compare:

| Input Length | gen_1 | gen_2 | gen_4 | gen_8 |
|-------------|--------|--------|--------|--------|
| 1 | 1.12B | 2.25B | 4.49B | 9.00B |
| 2 | 1.15B | 2.27B | 4.52B | 9.02B |
| 4 | 1.72B | 2.84B | 5.09B | 9.60B |
| 8 | 3.04B | 4.17B | 6.42B | 10.93B |
| 16 | 5.70B | 6.83B | 9.09B | 13.62B |
| 32 | 11.06B | 12.20B | 14.47B | 19.01B |
| 64 | 22.15B | 23.30B | 25.59B | 30.18B |
| 128 | 44.53B | 45.72B | 48.08B | 52.82B |
| 256 | 91.77B | 93.05B | 95.58B | 100.66B |
| 512 | 196.22B | 197.77B | 200.80B | 206.88B |
| 1024 | 445.26B | 445.26B | 445.26B | 445.26B |

The ratio one cycle to one instruction should be 1 cycle x 10.

## Cost related views
The model became inefficient when the input word were larger than 8 words and the output larger than 4 words. Sometimes the answer was totally wrong, sometimes the sentences were cut off or the same answer was listed twice. Moreover the costs increase much steeper when the word input is larger than 8. The output costs per word remains steady.

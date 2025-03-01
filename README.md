An overview what was changed and found for the ICP AI challenge repo.

As the advanced challenge the first AI challenge was chosen. The task was to deploy a GPT2 model and analyse costs and answers of the model.

For starting out the decide-ai-ic repo was forked on GitHub.

Then the requirements were installed on a Debian 12 VPS like described in the repo.

One change was made because Rust ws outdated:
"rustup target add wasm32-wasi" was changed to "rustup target add wasm32-wasip1". Any missing wasm packageswhich came up during installatin were installed as well. 
The dfx.json was changed accordingly and can be found in this repo.

The canister was started locally with "dfx start" and "dfx deploy". Different questions were checked for answers and cycles.

After checking some questions different quality was seen. The answers were sometimes correct, sometimes wrong and sometimes got different answers after retrying. The grammar and spelling was correct usually. Moreover GPT2 understood the questions in general. For instance a question about what is the highest mountain in Europe GPT2 was answered with "Mount Everest, Himalaya". The question what is the most popular coding language was answered with "Java" and sometimes with "Python". Questions about the capital of different countries were answered correctly. The question what could be the healthiest popular food were answered sometimes with "joghurt" and sometimes with a "rice meal". The output length made the answer more precise or descriptive. Sometimes the output length was to short because the sentence was not finished.

Table of cycles counted for different input and output length.

Input Length	gen_1	gen_2	gen_4	gen_8
1	1.12B	2.25B	4.49B	9.00B
2	1.15B	2.27B	4.52B	9.02B
4	1.72B	2.84B	5.09B	9.60B
8	3.04B	4.17B	6.42B	10.93B
16	5.70B	6.83B	9.09B	13.62B
32	11.06B	12.20B	14.47B	19.01B
64	22.15B	23.30B	25.59B	30.18B
128	44.53B	45.72B	48.08B	52.82B
256	91.77B	93.05B	95.58B	100.66B
512	196.22B	197.77B	200.80B	206.88B
1024	445.26B	445.26B	445.26B	445.26B

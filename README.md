 # Change this in Llama2 config


![image](https://github.com/DrishtiShrrrma/mixtral-8x7b-vs-mistral-vs-llama2-english-to-hinglish-translation/assets/129742046/6ea51b39-d450-45ab-a6cc-c00245e9a47e)


| Model | Training Loss | Epoch | Step | Validation Loss | Rouge Scores | Bleu Scores | Gen Len | Training Time (min) | GPU (Before Training) | Memory Reserved (Before Training) GB | Peak Reserved Memory GB | Peak Reserved Memory for Training GB | Peak Reserved Memory % of Max | Peak Reserved Memory for Training % of Max |
|-------|---------------|-------|------|-----------------|--------------|-------------|---------|---------------------|-----------------------|--------------------------------------|-------------------------|---------------------------------------|-------------------------------|---------------------------------------|
| llama-2-13b-fp16-english-to-hinglish-translation | 0.5477| 2.0 | 1000 | 0.7183 | {'rouge1': 0.9211071676780294, 'rouge2': 0.8281733381382788, 'rougeL': 0.8654973199305598, 'rougeLsum': 0.921063419066345} | [0.9430761623222732, 0.9291834498365306, 0.9116309260224186, 0.8930302852359673]| 2048| | | | | | | |
| llama-pro-8b-english-to-hinglish-translation | | | | | | | | | | | | | | |
| ... | | | | | | | | | | | | | | |




 embed this ingo in tabular format:

case 1: llama-2-13b-fp16-english-to-hinglish-translation

Training results
Training Loss	Epoch	Step	Validation Loss	Rouge Scores	Bleu Scores	Gen Len
0.7634	1.0	500	0.7242	{'rouge1': 0.9226356216479343, 'rouge2': 0.8298878258164286, 'rougeL': 0.8653820285905314, 'rougeLsum': 0.9225028041599788}	[0.9438235001535462, 0.9299872780706577, 0.9124966958220146, 0.8939299935025186]	2048.0
0.5477	2.0	1000	0.7183	{'rouge1': 0.9211071676780294, 'rouge2': 0.8281733381382788, 'rougeL': 0.8654973199305598, 'rougeLsum': 0.921063419066345}	[0.9430761623222732, 0.9291834498365306, 0.9116309260224186, 0.8930302852359673]	2048.0

training time, before training and after training stats are missing - please specify this only


case 2: llama-pro-8b-english-to-hinglish-translation

Training results
Training Loss	Epoch	Step	Validation Loss	Rouge Scores	Bleu Scores	Gen Len
0.8367	1.0	500	0.7705	{'rouge1': 0.9217534575496169, 'rouge2': 0.826045962480547, 'rougeL': 0.861202510859852, 'rougeLsum': 0.9217216485625217}	[0.07995984189186581, 0.07829715249738517, 0.07650957414005091, 0.07466840050021681]	2048.0
0.581	2.0	1000	0.7581	{'rouge1': 0.920395098520514, 'rouge2': 0.8260982220795346, 'rougeL': 0.8629699886603178, 'rougeLsum': 0.9203938314651259}	[0.0799874668395633, 0.07835910254936027, 0.07659241243282754, 0.0747653244473694]	2048.0

Training Time: 93.6060932358106 minutes


before training: # Show current memory stats
gpu_stats = torch.cuda.get_device_properties(0)
start_gpu_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
max_memory = round(gpu_stats.total_memory / 1024 / 1024 / 1024, 3)
print(f"GPU = {gpu_stats.name}. Max memory = {max_memory} GB.")
print(f"{start_gpu_memory} GB of memory reserved.")
GPU = NVIDIA A100 80GB PCIe. Max memory = 79.151 GB.
6.391 GB of memory reserved.


after training:  #@title Show final memory and time stats
used_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
used_memory_for_lora = round(used_memory - start_gpu_memory, 3)
used_percentage = round(used_memory         /max_memory*100, 3)
lora_percentage = round(used_memory_for_lora/max_memory*100, 3)
print(f"{trainer_stats.metrics['train_runtime']} seconds used for training.")
print(f"{round(trainer_stats.metrics['train_runtime']/60, 2)} minutes used for training.")
print(f"Peak reserved memory = {used_memory} GB.")
print(f"Peak reserved memory for training = {used_memory_for_lora} GB.")
print(f"Peak reserved memory % of max memory = {used_percentage} %.")
print(f"Peak reserved memory for training % of max memory = {lora_percentage} %.")
5612.9196 seconds used for training.
93.55 minutes used for training.
Peak reserved memory = 24.945 GB.
Peak reserved memory for training = 18.554 GB.
Peak reserved memory % of max memory = 31.516 %.
Peak reserved memory for training % of max memory = 23.441 %.


case 3: phi2-english-to-hinglish-translation

Training results
Training Loss	Epoch	Step	Validation Loss	Rouge Scores	Bleu Scores	Gen Len
1.6688	1.0	500	1.4150	{'rouge1': 0.021944939879946292, 'rouge2': 0.017781155558600512, 'rougeL': 0.017866554441667286, 'rougeLsum': 0.02197862373873669}	[0.014214089766333284, 0.013807603949625002, 0.013250971870467268, 0.012646602626664907]	2048.0
1.2148	2.0	1000	1.3394	{'rouge1': 0.02194963696306387, 'rouge2': 0.017844397420545253, 'rougeL': 0.017985463648805815, 'rougeLsum': 0.02198801722885821}	[0.0141983812922229, 0.013783602019353523, 0.013237039007079092, 0.012647324457245113]	2048.0

Training Time: 124.70718178749084 minutes

before training: # Show current memory stats
gpu_stats = torch.cuda.get_device_properties(0)
start_gpu_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
max_memory = round(gpu_stats.total_memory / 1024 / 1024 / 1024, 3)
print(f"GPU = {gpu_stats.name}. Max memory = {max_memory} GB.")
print(f"{start_gpu_memory} GB of memory reserved.")
GPU = NVIDIA A100 80GB PCIe. Max memory = 79.199 GB.
3.084 GB of memory reserved.

after training: #@title Show final memory and time stats
used_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
used_memory_for_lora = round(used_memory - start_gpu_memory, 3)
used_percentage = round(used_memory         /max_memory*100, 3)
lora_percentage = round(used_memory_for_lora/max_memory*100, 3)
print(f"{trainer_stats.metrics['train_runtime']} seconds used for training.")
print(f"{round(trainer_stats.metrics['train_runtime']/60, 2)} minutes used for training.")
print(f"Peak reserved memory = {used_memory} GB.")
print(f"Peak reserved memory for training = {used_memory_for_lora} GB.")
print(f"Peak reserved memory % of max memory = {used_percentage} %.")
print(f"Peak reserved memory for training % of max memory = {lora_percentage} %.")
7479.4644 seconds used for training.
124.66 minutes used for training.
Peak reserved memory = 29.822 GB.
Peak reserved memory for training = 26.738 GB.
Peak reserved memory % of max memory = 37.655 %.
Peak reserved memory for training % of max memory = 33.761 %.

case 4: mistral-7b-v0.1-english-to-hinglish-translation

Training results
Training Loss	Epoch	Step	Validation Loss	Rouge Scores	Bleu Scores	Gen Len
0.9667	1.0	500	0.8997	{'rouge1': 0.9066197962103982, 'rouge2': 0.7949438120742293, 'rougeL': 0.8365583570941119, 'rougeLsum': 0.906542182776239}	[0.9280923249970773, 0.9116476390859075, 0.8901882800412136, 0.8671907395641425]	2048.0
0.5702	2.0	1000	0.9017	{'rouge1': 0.9052154858930703, 'rouge2': 0.7938118811886605, 'rougeL': 0.8365543601879399, 'rougeLsum': 0.9051011676969527}	[0.9286814242037147, 0.9121661008968365, 0.8907823041130339, 0.8677722819236368]	2048.0

Training Time: 69.46867498159409 minutes

before training: # Show current memory stats
gpu_stats = torch.cuda.get_device_properties(0)
start_gpu_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
max_memory = round(gpu_stats.total_memory / 1024 / 1024 / 1024, 3)
print(f"GPU = {gpu_stats.name}. Max memory = {max_memory} GB.")
print(f"{start_gpu_memory} GB of memory reserved.")
GPU = NVIDIA A100 80GB PCIe. Max memory = 79.199 GB.
6.1 GB of memory reserved.

after training: #@title Show final memory and time stats
used_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
used_memory_for_lora = round(used_memory - start_gpu_memory, 3)
used_percentage = round(used_memory         /max_memory*100, 3)
lora_percentage = round(used_memory_for_lora/max_memory*100, 3)
print(f"{trainer_stats.metrics['train_runtime']} seconds used for training.")
print(f"{round(trainer_stats.metrics['train_runtime']/60, 2)} minutes used for training.")
print(f"Peak reserved memory = {used_memory} GB.")
print(f"Peak reserved memory for training = {used_memory_for_lora} GB.")
print(f"Peak reserved memory % of max memory = {used_percentage} %.")
print(f"Peak reserved memory for training % of max memory = {lora_percentage} %.")
4164.9145 seconds used for training.
69.42 minutes used for training.
Peak reserved memory = 24.719 GB.
Peak reserved memory for training = 18.619 GB.
Peak reserved memory % of max memory = 31.211 %.
Peak reserved memory for training % of max memory = 23.509 %


case 5: llama2-7b-english-to-hinglish-translation

Training results
Training Loss	Epoch	Step	Validation Loss	Rouge Scores	Bleu Scores	Gen Len
0.8283	1.0	500	0.7644	{'rouge1': 0.921717672607307, 'rouge2': 0.8269254584175559, 'rougeL': 0.8617480706939217, 'rougeLsum': 0.9216499826848323}	[0.9428124451183093, 0.9288838577090098, 0.910999858543974, 0.8919623155075178]	2048.0
0.5824	2.0	1000	0.7508	{'rouge1': 0.9207934134490793, 'rouge2': 0.8268216875143521, 'rougeL': 0.863418556340243, 'rougeLsum': 0.9207165318568765}	[0.9430535279899742, 0.9289517504059885, 0.9111307023404618, 0.8922236591496603]	2048.0

Training Time: 57.71269731124242 minutes

before training: # Show current memory stats
gpu_stats = torch.cuda.get_device_properties(0)
start_gpu_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
max_memory = round(gpu_stats.total_memory / 1024 / 1024 / 1024, 3)
print(f"GPU = {gpu_stats.name}. Max memory = {max_memory} GB.")
print(f"{start_gpu_memory} GB of memory reserved.")
GPU = NVIDIA A100 80GB PCIe. Max memory = 79.15 GB.
5.314 GB of memory reserved.


after training:  #@title Show final memory and time stats
used_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
used_memory_for_lora = round(used_memory - start_gpu_memory, 3)
used_percentage = round(used_memory         /max_memory*100, 3)
lora_percentage = round(used_memory_for_lora/max_memory*100, 3)
print(f"{trainer_stats.metrics['train_runtime']} seconds used for training.")
print(f"{round(trainer_stats.metrics['train_runtime']/60, 2)} minutes used for training.")
print(f"Peak reserved memory = {used_memory} GB.")
print(f"Peak reserved memory for training = {used_memory_for_lora} GB.")
print(f"Peak reserved memory % of max memory = {used_percentage} %.")
print(f"Peak reserved memory for training % of max memory = {lora_percentage} %.")
3459.2632 seconds used for training.
57.65 minutes used for training.
Peak reserved memory = 42.266 GB.
Peak reserved memory for training = 36.952 GB.
Peak reserved memory % of max memory = 53.4 %.
Peak reserved memory for training % of max memory = 46.686 %.


case 6: mixtral-8x7b-v0.1-english-to-hinglish-translation

Training results
Training Loss	Epoch	Step	Validation Loss	Rouge Scores	Bleu Scores	Gen Len
1.1771	1.0	500	1.0579	{'rouge1': 0.9070255400902434, 'rouge2': 0.7976770190068221, 'rougeL': 0.8400261479965636, 'rougeLsum': 0.9069363147075731}	[0.00028395954091190866, 0.0002796973368739713, 0.0002722057765709132, 0.000263740024418467]	2047.996
0.7788	2.0	1000	1.0769	{'rouge1': 0.90.45408202972536, 'rouge2': 0.795425441228359, 'rougeL': 0.8399846297860634, 'rougeLsum': 0.9043739034131012}	[0.0002881182166187815, 0.0002842750061873772, 0.0002764768847375588, 0.00026750640347869873]	2048.0

Training Time: 190.16621324618657 minutes

before training: # Show current memory stats
gpu_stats = torch.cuda.get_device_properties(0)
start_gpu_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
max_memory = round(gpu_stats.total_memory / 1024 / 1024 / 1024, 3)
print(f"GPU = {gpu_stats.name}. Max memory = {max_memory} GB.")
print(f"{start_gpu_memory} GB of memory reserved.")
GPU = NVIDIA A100 80GB PCIe. Max memory = 79.199 GB.
29.957 GB of memory reserved.

after training: #@title Show final memory and time stats
used_memory = round(torch.cuda.max_memory_reserved() / 1024 / 1024 / 1024, 3)
used_memory_for_lora = round(used_memory - start_gpu_memory, 3)
used_percentage = round(used_memory         /max_memory*100, 3)
lora_percentage = round(used_memory_for_lora/max_memory*100, 3)
print(f"{trainer_stats.metrics['train_runtime']} seconds used for training.")
print(f"{round(trainer_stats.metrics['train_runtime']/60, 2)} minutes used for training.")
print(f"Peak reserved memory = {used_memory} GB.")
print(f"Peak reserved memory for training = {used_memory_for_lora} GB.")
print(f"Peak reserved memory % of max memory = {used_percentage} %.")
print(f"Peak reserved memory for training % of max memory = {lora_percentage} %.")
11406.6945 seconds used for training.
190.11 minutes used for training.
Peak reserved memory = 74.137 GB.
Peak reserved memory for training = 44.18 GB.
Peak reserved memory % of max memory = 93.609 %.
Peak reserved memory for training % of max memory = 55.784 %.


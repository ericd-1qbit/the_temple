#pathologies: ['Atelectasis', 'Consolidation', 'Infiltration', 'Pneumothorax', 'Edema', 'Emphysema', 'Fibrosis', 'Effusion', 'Pneumonia', 'Pleural_Thickening', 'Cardiomegaly', 'Nodule', 'Mass', 'Hernia']


```  

def get_sampled_images_paths(images_path: str) -> list[str]:

return glob.glob(images_path + "/*.png")

  
  

def get_synthetic_dataset() -> Type[BaseDataset]:

# TODO these are dummies to retain the previously implemented structure

# raise NotImplementedError()

return None

  
  

def get_mixed_dataset() -> Type[BaseDataset]:

# TODO these are dummies to retain the previously implemented structure

# real_dataset: Type[BaseDataset], synthetic_dataset: Type[BaseDataset]

# return torch.utils.data.ConcatDataset([real_dataset, synthetic_dataset])

return None

  
  

def get_dataset(dataset_flavour: str, config: DictConfig) -> Type[BaseDataset]:

"""Get the requested dataset mixture. Real, Synthetic or Real+Synthetic.

  

Args:

dataset_flavour (str): which dataset scenario to choose

  

Raises:

Exception: raises Exception of scenario unknown.

  

Returns:

Type[BaseDataset]: final assembled dataset.

"""

  

real_dataset_class = get_dataset_class(config.dataset.dataset_name)

  

if dataset_flavour.lower() == "real":

dataset = real_dataset_class(**config.dataset)

elif dataset_flavour.lower() == "synthetic":

dataset = get_synthetic_dataset()

elif dataset_flavour.lower() == "real+synthetic":

dataset = get_mixed_dataset()

else:

raise Exception(f"Unknown dataset scenario {dataset_flavour}.")

  

return dataset
  

for dataset_flavour in config.evaluator.classifier_perf.dataset_flavours:

dataset = get_dataset(dataset_flavour, config=config)

if not dataset:

logging.warning(

f"Dataset flavour {dataset_flavour} not implemented. Skipping."

)

continue

  

# create the train and test data loaders

test_length = int(classifier_cfg.dataset_test_split * len(dataset))

train_length = len(dataset) - test_length

  

train_dataset, test_dataset = random_split(

dataset=dataset,

lengths=[train_length, test_length],

generator=torch.Generator().manual_seed(classifier_cfg.dataset_split_seed),

)

# TODO use common functionality

# create the train and test data loaders

# train_data_loader, test_data_loader = create_train_test_data_loader(

# world_size=world_size, rank=rank, dataset=dataset, config=config

# )

train_data_loader = create_data_loader_from_dataset(

dataset=train_dataset,

rank=rank,

world_size=world_size,

logging=logging,

**config.dataset,

)

test_data_loader = create_data_loader_from_dataset(

dataset=test_dataset,

rank=rank,

world_size=world_size,

logging=logging,

**config.dataset,

)

# train and test the classifier on the original data set

train_classifier(

is_first_gpu,

classifier,

train_data_loader,

config.evaluator.classifier_perf,

)










  

def test_classifier(self, test_data_loader: DataLoader) -> None:

# correct = 0

# total = 0

# # since we're not training, we don't need to calculate the gradients for our outputs

# with torch.no_grad():

# for data in test_data_loader:

# images, labels = data

# # calculate outputs by running images through the network

# outputs = model(images)

# # the class with the highest energy is what we choose as prediction

# _, predicted = torch.max(outputs.data, 1)

# total += labels.size(0)

# correct += (predicted == labels).sum().item()

  

# print(

# f"Accuracy of the network on the 10000 test images: {100 * correct // total} %"

# )

  

# return 0.0

raise NotImplementedError()
```
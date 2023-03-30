```



# overwrite parameters from hyperparameters config file (NOTE: names should be the same in train and hyperparameters configs.)

if hyperparameters:

for hp_name in hyperparameters.keys():

configs.trainer[hp_name] = hyperparameters[hp_name]


if is_first_gpu and configs.general.use_hyperopt and configs.general.use_mlflow:

helpers_hyperopt.save_mlflow_run_id(context_manager.mlflow_run_id)


from hyperopt import Trials, fmin, tpe

if use_hyperopt:

  

# the variable "trials" stores various setups that hyperopt uses, enabling us to retrieve our run_id from this object.

trials = Trials()

  

hyperopt_param_space = {

"trainer_fn": main,

"distributed": distributed,

"use_mlflow": use_mlflow,

"world_size": world_size,

"configs": configs,

"evaluation_configs": configs,

"hyperparameters": helpers_hyperopt.hyperopt_param_space_generator(

hp_config=configs.hyperparameters

),

}

  

# run hyperopt

fmin(

fn=helpers_hyperopt.hyperopt_param_objective_fn,

space=hyperopt_param_space,

trials=trials,

algo=tpe.suggest,

max_evals=helpers_hyperopt.space_size(

hyperopt_param_space["hyperparameters"]

),

)

  

best_fid, best_trial = min(

(trial["result"]["loss"], trial) for trial in trials.trials

)

  

logging.info(f"The best FID score is: {best_fid}")

logging.info(

f"The best hyperparameter set for minimizing FID score is: {best_trial}"

)

```
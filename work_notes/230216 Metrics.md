
Difference between multi-class classification & multi-label classification is that **in multi-class problems the classes are mutually exclusive, whereas for multi-label problems each label represents a different classification task, but the tasks are somehow related**.

    # Precision: 0.28483283519744873
    # Accuracy: 0.8246626257896423
    # AUROC: 0.9272322058677673



    # if "normal" in pathologies:
    #     assert (
    #         len(pathologies) == 1
    #     ), f"Image tagged normal but full pathology list {pathologies}."

    #     target = torch.zeros_like(prediction[0])

    # output["preds"] = dict(
    #     zip(xrv.datasets.default_pathologies, prediction[0].detach().numpy())
    # )
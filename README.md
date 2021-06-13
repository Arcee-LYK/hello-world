# 对抗攻击与防御

除源代码中已有py文件，新增py文件如下：

    攻击部分：newpgd_attack:对pgd算法的改进，用于攻击除model3以外的其他五个模型，使用时在attack_main里直接调用 attack = PGDDLR(args.epsilon)
             ADVGAN_attack:基于GAN的攻击算法,用于model3的攻击，使用时在attack_main里直接调用 attack = AD(args.step_size,args.epsilon,args.perturb_steps,device)
             cw_attack：不作为攻击模型，使用时在attack_main里直接调用attack = CW(args.perturb_steps,args.epsilon)
    
    防御部分：defense_model:自定义的神经网络defense_net，在attack_main中已将防御模型和参数更改为defense_net和其对应的参数
             train:由pgd_train修改而来，用于对defense_net的训练
             infer:对cifar-10数据集的测试集在defense_net上直接进行分类，可直接运行得到分类结果
             
对原有代码的修改如下：

    pgd_train重命名为train，且内部训练模型已切换为defense_net模型
    attack_main中的防御模型已切换为defense_net模型

训练的防御模型的weight在models/weights文件夹下（my_defence_e99_0.7928_0.4840-final.pt）

当前attack_main中的攻击算法为改进后的pgd算法，为确保可顺利运行，“gpu_id”已更改为0，可直接运行，若要运行其余攻击算法，请手动取消对应的注释。

提交的代码中已下载好cifar-10数据集。

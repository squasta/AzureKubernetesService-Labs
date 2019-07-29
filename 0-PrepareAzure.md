
#  ___                                _                    
# | _ \_ _ ___ _ __  __ _ _ _ ___    /_\   ____  _ _ _ ___ 
# |  _/ '_/ -_) '_ \/ _` | '_/ -_)  / _ \ |_ / || | '_/ -_)
# |_| |_| \___| .__/\__,_|_| \___| /_/ \_\/__|\_,_|_| \___|
#             |_|                                          

==============================================================
= Version 1.0
= Stanislas
= genere ici : http://patorjk.com/software/taag/#p=display&f=Small&t=AKS%20deployment
==============================================================

# Documentation : https://docs.microsoft.com/en-us/cli/azure/ext/aks-preview/aks?view=azure-cli-latest#ext-aks-preview-az-aks-create

# add aks extension for AKS preview feature
az extension add --name aks-preview
az extension update --name aks-preview

# register for AKS preview features
az feature register -n WindowsPreview --namespace Microsoft.ContainerService
az feature register -n AKSLockingDownEgressPreview --namespace Microsoft.ContainerService
az feature register -n MultiAgentpoolPreview --namespace Microsoft.ContainerService
az feature register -n APIServerSecurityPreview --namespace Microsoft.ContainerService
az feature register -n VMSSPreview --namespace Microsoft.ContainerService
az feature register --name AKSAuditLog --namespace Microsoft.ContainerService
az feature register --name PodSecurityPolicyPreview --namespace Microsoft.ContainerService
az feature register --namespace "Microsoft.ContainerService" --name "AKSAzureStandardLoadBalancer"
az feature register --namespace "Microsoft.ContainerService" --name "AvailabilityZonePreview"
az feature register --namespace "Microsoft.ContainerService" --name "EnableNetworkPolicy"

# Check registration state for all aks preview features
az feature list -o table --query "[?contains(name, 'Microsoft.ContainerService/')].{Name:name,State:properties.state}"

# /!\ only When all feature are marked as Registered, ReRegister ContainerService provider
az provider register -n Microsoft.ContainerService

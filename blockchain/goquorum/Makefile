setup-ingress-nginx:
	helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
	helm repo update
	helm install quorum-network-ingress ingress-nginx/ingress-nginx \
		--namespace quorum \
		--set controller.ingressClassResource.name="network-nginx" \
		--set controller.ingressClassResource.controllerValue="k8s.io/network-ingress-nginx" \
		--set controller.replicaCount=1 \
		--set controller.nodeSelector."kubernetes\.io/os"=linux \
		--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
		--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
		--set controller.service.externalTrafficPolicy=Local
setup-monitoring:
	helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
	helm repo update
	# NOTE: please refer to values/monitoring.yml to configure the alerts per your requirements ie slack, email etc
	helm install prometheus-operator prometheus-community/kube-prometheus-stack --namespace=quorum --create-namespace --wait
	kubectl --namespace quorum apply -f ./quorum-kubernetes/helm/values/monitoring/grafana-goquorum-dashboard.yml

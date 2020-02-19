# jsonpath-101
Sample scripts for jsonpath
*Basic Jsonpath*

kubectl get nodes -o=jsonpath='{.items[*].metadata.name}' //Remember here we need to use .items[*] to fetch all the nodes

kubectl get nodes -o=jsonpath='{range .items[*]} {"\n" }{.metadata.name}{end} {"\n"}'

* Making use of RegEx and also conditioning the results from the array, parsing the dictionary inside the array*

kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='fine-user')].name}"


*kubectl support with --sort-by and custom-columns does not need to provide .items[*] as it get these details implicitly.*

kubectl get pv --sort-by=.spec.capacity.storage -o=custom-columns=NAME:.metadata.name,-o=custom-columns=CAPACITY:.spec.capacity.storage

kubectl get pods --all-namespaces --sort-by='{.metadata.name}' -o=custom-columns=PODNAME:.metadata.name,PODNAMESPACE:.metadata.name
spaces
 
kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='-user')].name}" > /opt/outputs/aws-context-name


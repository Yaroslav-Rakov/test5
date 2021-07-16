Порядок выполнения действий:

1. Клонировать репозиторий: git clone https://github.com/Yaroslav-Rakov/test5.git

2. Перейти в директорию test5/myapp: cd test5/myapp

3. Сбилдить образ из Dockerfile c тэгом gdust/test5: sudo docker build -t gdust/test5 .

4. Перейти в директорию test5: cd ..

5. Создать deployment для Helloworld Node.js сервиса с 2-мя репликами из файла myapp.yml: kubectl apply -f myapp.yml

6. Создать сервис test5: kubectl expose deployment test5 --type=NodePort --port=8000

7. Проверить сервис: minikube service test5 (откроется браузер с Hello World!)

8. Проверить, чтобы наши deployment с репликами и сервисами горели зеленым в minikube dashboard: запустить в новом терминале minikube dashboard (откроется браузер)

9. Запустить myingress.yml, который будет отправлять трафик на сервис test5 через hello-world.info: kubectl apply -f myingress.yml

10. Проверить IP адрес через kubectl get ingress либо через minikube dashboard (например, мы получили IP: 172.17.0.15) 

11. Добавить 172.17.0.15 hello-world.info в конец /etc/hosts файла (у вас может быть другой IP, который вы получили через kubectl get ingress)

12. Проверить, что Ingress controller направляет трафик: curl hello-world.info (должны увидеть Hellow World! в терминале)

Дополнительная информация со всеми необходимыми файлами .yml отдельно вынесена в gist: https://gist.github.com/Yaroslav-Rakov/159733f7e4d2c737179a80207674d5ee 







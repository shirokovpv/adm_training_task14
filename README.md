# adm_training_task14
<h1 align="center">Занятие 14. Docker</h1>
<h3 class="western"><a name="_heading=h.h6i87lkp3f19"></a> <span style="font-family: Roboto, serif;"><span style="font-size: small;">Описание домашнего задания</span></span></h3>
<ol>
<li style="font-weight: 300;"><span style="font-weight: 300;">Установите Docker на хост машину</span></li>
<p><a href="https://docs.docker.com/engine/install/ubuntu/"><span style="font-weight: 300;">https://docs.docker.com/engine/install/ubuntu/</span></a></p>
<li style="font-weight: 300;"><span style="font-weight: 300;">Установите Docker Compose - как плагин, или как отдельное приложение</span></li>
<li style="font-weight: 300;"><span style="font-weight: 300;">Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx)</span></li>
<li style="font-weight: 300;"><span style="font-weight: 300;">Определите разницу между контейнером и образом</span></li>
<li style="font-weight: 300;"><span style="font-weight: 300;">Вывод опишите в домашнем задании.</span></li>
<li style="font-weight: 300;"><span style="font-weight: 300;">Ответьте на вопрос: Можно ли в контейнере собрать ядро?</span></li>
</ol>
<p><span style="font-weight: 300;">Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий.</span></p>
<h3 class="western"><a name="_heading=h.df570rpzx1qg"></a><span style="font-family: Roboto, serif;"><span style="font-size: small;">Используемые ОС</span></span></h3>
<p style="line-height: 108%; margin-bottom: 0.28cm;" align="justify"><span style="font-family: Roboto, serif;">Хостовая ОС: Ubuntu 24.04 Desktop.</span></span></p>
<h3 class="western"><span style="font-family: Roboto, serif;"><span style="font-size: small;">Выполнение</span></span></h3>
<p>На машине установлен Docker и Docker Compose:</p>
<img width="618" height="693" alt="image" src="https://github.com/user-attachments/assets/6f0f7adc-5489-4bb5-9c3d-625f250e8f7b" />
<p>&nbsp;</p>
<p dir="auto">Создаем директорию:</p>
<p dir="auto">mkdir /nginx_custom ; cd /nginx_custom</p>
<img width="618" height="58" alt="image" src="https://github.com/user-attachments/assets/ad5a505d-0962-4e15-9fd2-26cb182342f2" />
<p>&nbsp;</p>
<p dir="auto">Создаем Dockerfile и index.html</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto">
<pre class="notranslate"><code>
echo 'FROM nginx:alpine
COPY ./index.html /usr/share/nginx/html/index.html' &gt; Dockerfile ;
echo '&lt;h1&gt;&lt;center&gt;Hello Everyone!&lt;/center&gt;&lt;/h1&gt;' &gt; index.html&nbsp;
</code></pre>
</div>
<img width="669" height="202" alt="image" src="https://github.com/user-attachments/assets/d11af56e-7343-4360-9adb-cd4f540a95f3" />
<p>&nbsp;</p>
<p dir="auto">Создаем контейнер:</p>
<p dir="auto"><code>docker build -t nginx_custom .</code></p>
<img width="806" height="800" alt="image" src="https://github.com/user-attachments/assets/b6b599ee-e13c-41d2-ad75-4199886cca26" />
<p>&nbsp;</p>
<p dir="auto">Запуск контейнера:</p>
<p dir="auto"><code>docker run -d --name webserver -p 8080:80 nginx_custom</code></p>
<p dir="auto">Вывод docker ps и результат curl по локалхост :</p>
<p dir="auto"><code>docker ps ; curl 127.0.0.1:8080</code></p>
<img width="1401" height="167" alt="image" src="https://github.com/user-attachments/assets/ad6dc94b-021c-4879-bae3-de3ab1bb4cb1" />
<p>&nbsp;</p>
<p>Подключаемся к к Docker Hub:</p>
<img width="826" height="316" alt="image" src="https://github.com/user-attachments/assets/f55b2036-ab83-42c8-95de-b9aeb9f6416b" />
<p>&nbsp;</p>
<p dir="auto">Прикрепим tag на образ:</p>
<p dir="auto"><code>docker tag nginx_custom shirokovpv/nginx_custom:latest</code></p>
<p dir="auto">Выполним загрузку Docker-образа на Docker Hub:</p>
<p dir="auto"><code>docker push shirokovpv/nginx_custom:latest</code></p>
<img width="992" height="316" alt="image" src="https://github.com/user-attachments/assets/bd8653ef-1ae9-426c-985e-4e6bcea16632" />
<p>&nbsp;</p>
<img width="1835" height="868" alt="image" src="https://github.com/user-attachments/assets/41db28c1-8646-40ba-8393-670a64ca3cda" />
<p>&nbsp;</p>
<p dir="auto">Останавливаем, удаляем, проверяем наличие:</p>
<p dir="auto"><code>docker ps; docker stop c96774695088 ; docker rmi -f c96774695088 ; docker images</code></p>
<img width="1102" height="229" alt="image" src="https://github.com/user-attachments/assets/5dc0467c-c4f3-42dd-9569-92c948705e8e" />
<p>&nbsp;</p>
<p dir="auto">Видим, что nginx_custom отсутствует.</p>
<p dir="auto">Скачиваем обратно образ и запускаем:</p>
<p dir="auto"><code>docker pull shirokovpv/nginx_custom ; docker run -d --name webserv -p 8080:80 shirokovpv/nginx_custom</code></p>
<p dir="auto">Финальная проверка:</p>
<p dir="auto"><code>curl 127.0.0.1:8080</code></p>
<img width="1299" height="432" alt="image" src="https://github.com/user-attachments/assets/a7523baa-698f-43b1-8952-475f8df3d2bc" />
<p>&nbsp;</p>
<p dir="auto"><code>docker images</code></p>
<img width="776" height="116" alt="image" src="https://github.com/user-attachments/assets/5f70c9b1-554b-4f29-8b2e-49ef75cd9cec" />
<p>&nbsp;</p>
<p dir="auto">Видим, что nginx_custom снова на месте.</p>
<p dir="auto">Собрать новое ядро в Linux-контейнере нельзя (даже с флагом --privileged), поскольку контейнер не имеет собственного ядра, а использует ядро хостовой операционной системы. Контейнер лишь создает изолированное рабочее пространство на основе процессов и файловой системы, опираясь на функциональность существующего ядра Linux. Это не виртуальная машина.<span class="" data-wiz-rootname="ohfaMd"><span class="vKEkVd" data-animation-atomic="">&nbsp;</span></span></p>
<p dir="auto">Docker-образ — это неизменяемый шаблон, который содержит всё необходимое для запуска приложения: его код, среду выполнения, библиотеки, переменные окружения и конфигурационные файлы. Это исполняемый пакет, из которого создаются Docker-контейнеры.</p>
<p dir="auto">Docker-контейнер — это стандартизированная, изолированная и портативная среда выполнения, содержащая все необходимое для запуска приложения, включая код, библиотеки и зависимости. Контейнер представляет собой запущенный экземпляр Docker-образа и работает на уровне ядра операционной системы хоста, используя его ресурсы.</p>
<p dir="auto">Задание завершено.</p>

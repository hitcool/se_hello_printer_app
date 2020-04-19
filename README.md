# Simple Flask App

Aplikacja Dydaktyczna wyświetlająca imię i wiadomość w różnych formatach dla zajęć
o Continuous Integration, Continuous Delivery i Continuous Deployment.

- W projekcie wykorzystamy virtual environment, dla utworzenia hermetycznego środowisko dla aplikacji:

  ```
  # tworzymy hermetyczne środowisko dla bibliotek aplikacji:
  $ python3 -m venv .venv

  # aktywowanie hermetycznego środowiska
  $ source .venv/bin/activate
  $ pip install -r requirements.txt
  $ pip install -r test_requirements.txt

  # zobacz
  $ pip list
  ```

  Sprawdź: [tutorial venv](https://docs.python.org/3/tutorial/venv.html) oraz [biblioteki flask](http://flask.pocoo.org).

- Uruchamianie applikacji:

  ```
  # jako zwykły program
  $ python main.py

  # albo:
  $ PYTHONPATH=. FLASK_APP=hello_world flask run
  ```

- Uruchamianie testów (see: http://doc.pytest.org/en/latest/capture.html):

  ```
  $ PYTHONPATH=. py.test
  $ PYTHONPATH=. py.test --verbose -s
  ```

- Kontynuując pracę z projektem, aktywowanie hermetycznego środowiska dla aplikacji py:

  ```
  # deaktywacja
  $ deactivate
  ```

  ```
  ...

  # aktywacja
  $ source .venv/bin/activate
  ```

- Integracja z TravisCI:

  ```
  # miejsce na twoje notatki
  ```

  -------------20200418------------------
- Dodany plik Makefile w którym wpisujemy:
  # aby uruchomić w terminalu wpisujemy: make deps, make run, make lint
  .PHONY: test

  deps:
  	pip install -r requirements.txt; \
  	pip install -r test_requirements.txt

  lint:
  	flake8 hello_world test

  run:
  	PYTHONPATH=. FLASK_APP=hello_world flask run

  test:
  	PYTHONPATH=. py.test --verbose -s

  docker_build:
  	docker build -t hello-world-printer .
  ----------------------------------------



# Pomocnicze

## Ubuntu

-----------------------------------------
5.
- Instalacja dockera: [dockerce howto](https://docs.docker.com/install/linux/docker-ce/ubuntu/)



- 2 Instalacja docker-a:

FROM python:3
ARG APP_DIR=/usr/src/hello_world_printer
WORKDIR /tmp
ADD requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt
RUN mkdir -p $APP_DIR
ADD hello_world/ $APP_DIR/hello_world/
ADD main.py $APP_DIR

CMD PYTHONPATH=$PYTHONPATH:/usr/src/hello_world_printer \
  FLASK_APP=hello_world flask run --host=0.0.0.0

------------------------
- 3. w nowej konsoli sudo su uruchamiamy:
  make decker_build
- 4. Jeśli komponent jest prosty, możemy weryfikować poprawność definicji w czasie etapu budowy:
Zmień CMD na RUN i ponownie zbuduj komponent. Jeśli aplikacja się uruchomiła, powróć do poprzedniej wersji Dockerfile.

------------------------
- 6. Uruchom hello-world-printer jako docker, w terminalu:
make docker_run
# zweryfikuj, że docker jest uruchomiony
docker ps
# sprawdź czy aplikacje działa poprawnie
curl 127.0.0.1:5000

------------------------
Docker zazwyczaj nie restartujemy, kasujemy i uruchamiamy na nowo:
# docker stop hello-world-printer-dev
# docker rm hello-world-printer-dev
# make docker_run

------------------------
    Przydatne komendy docker-a (pamiętamy o sudo):
    # możemy uruchomieć basha w naszym dockerze
    docker run -it hello-world-printer /bin/bash
    # uruchamiamy bash-a w działającym dockerze z naszą aplikcją:
    docker exec -it hello-world-printer-dev /bin/bash




-----------------------------------------
## Centos

  ```
  $ yum remove docker \
        docker-common \
        container-selinux \
        docker-selinux \
        docker-engine

  $ yum install -y yum-utils

  $ yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo

  $ yum makecache fast
  $ yum install -y docker-ce
  $ systemctl start docker
  ```

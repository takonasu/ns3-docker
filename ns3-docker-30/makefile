NAME=docker-ns3-34

build: Dockerfile
	if [ -d "./ns-allinone-3.34" ]; then \
		echo "Dir exists, skip downloading .."; \
	else \
		wget https://www.nsnam.org/releases/ns-allinone-3.34.tar.bz2; \
		tar -xf ./ns-allinone-3.34.tar.bz2; \
		rm ./ns-allinone-3.34.tar.bz2; \
	fi
	docker build -t $(NAME) .

run:
	docker run --rm -it -v `pwd`/ns-allinone-3.34/ns-3.34/src/:/usr/ns3/ns-3.34/src -e DISPLAY=docker.for.mac.host.internal:0 $(NAME)
build: Dockerfile
	if [ -d "./ns-allinone-3.35" ]; then \
		echo "Dir exists, skip downloading .."; \
	else \
		wget https://www.nsnam.org/releases/ns-allinone-3.35.tar.bz2; \
		tar -xf ./ns-allinone-3.35.tar.bz2; \
		rm ./ns-allinone-3.35.tar.bz2; \
	fi
	docker-compose up -d
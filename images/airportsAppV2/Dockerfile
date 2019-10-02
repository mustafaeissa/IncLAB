FROM openjdk:8
ENV airAPP airports-assembly-1.1.0.jar
ADD $airAPP  /opt/$airAPP
ENTRYPOINT ["sh", "-c", "java", "-jar", "/opt/$airAPP"]


# GRPConARM32

This repo contains the binaries that are used to compile GRPC .proto files into .java on a arm32 device

To install on your local maven repository do the following:

```bash
git clone https://github.com/Iqop/GRPConARM32
cd GRPConARM32
mkdir -p ~/.m2/repository/io/grpc/protoc-gen-grpc-java/1.34.0/
mkdir -p ~/.m2/repository/com/google/protobuf/protoc/3.12.4/
cp protoc-gen-grpc-java-1.34.0-linux-arm_32.exe ~/.m2/repository/io/grpc/protoc-gen-grpc-java/1.34.0/
cp protoc-3.12.4-linux-arm_32.exe ~/.m2/repository/com/google/protobuf/protoc/3.12.4/
unzip libprotoc.so.zip
cp libprotoc.so /usr/lib/
```
With this the following plugin configuration can find the compiled binaries

```
      <plugin>
        <groupId>org.xolstice.maven.plugins</groupId>
        <artifactId>protobuf-maven-plugin</artifactId>
        <version>0.6.1</version>
        <configuration>
          <protocArtifact>com.google.protobuf:protoc:3.12.4:exe:${os.detected.classifier}</protocArtifact>
          <pluginId>grpc-java</pluginId>
          <pluginArtifact>io.grpc:protoc-gen-grpc-java:1.34.0:exe:${os.detected.classifier}</pluginArtifact>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>compile</goal>
              <goal>compile-custom</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
```

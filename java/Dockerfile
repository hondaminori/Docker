# Maven 3.9 + Temurin JDK 17（Eclipse Adoptium）の公式イメージを使用
FROM maven:3.9.6-eclipse-temurin-17

# 作業ディレクトリを設定（任意のアプリ配置場所）
WORKDIR /usr/src/app

# Mavenキャッシュを生かすため pom.xml とソースを分けてコピー
COPY pom.xml ./
RUN mvn dependency:go-offline

# ソースコードをコピー
COPY src ./src

# デフォルトのコマンド（bashで起動）
CMD ["bash"]
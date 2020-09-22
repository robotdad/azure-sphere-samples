FROM mcr.microsoft.com/azurespheresdk:latest AS dev
RUN curl -L -O https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2019q4/gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2 && \
    tar -xf gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2 && \
    rm gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2;
ENV PATH "$PATH:/:/gcc-arm-none-eabi-9-2019-q4-major/bin"

FROM dev AS build
COPY ./ /src/
WORKDIR /out
RUN cmake -G "Ninja" -DCMAKE_TOOLCHAIN_FILE="/opt/azurespheresdk/CMakeFiles/AzureSphereToolchain.cmake" \
    -DAZURE_SPHERE_TARGET_API_SET="latest-lts" -DCMAKE_BUILD_TYPE="Release" "/src"
ENTRYPOINT [ "ninja" ]
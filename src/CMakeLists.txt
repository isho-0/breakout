# 소스 파일
set(SOURCES
    main.cc
    shader.cc
    texture.cc
    resource_manager.cc
    game.cc
    stb_image.h
)

# 헤더 파일
set(HEADERS
    shader.h
    texture.h
    resource_manager.h
    game.h
)

# OpenGL과 GLFW 라이브러리 찾기
find_package(OpenGL REQUIRED)

# Homebrew로 설치된 GLFW와 GLM 찾기
set(CMAKE_PREFIX_PATH "/opt/homebrew/opt/glfw;/opt/homebrew/opt/glm")
find_package(glfw3 REQUIRED)
find_package(glm REQUIRED)

# 실행 파일
add_executable(breakout ${SOURCES} ${HEADERS})

# 헤더 파일 경로 설정
target_include_directories(breakout PRIVATE 
    ${CMAKE_CURRENT_SOURCE_DIR}
    /opt/homebrew/Cellar/glm/1.0.1/include
)

# STB 이미지 라이브러리 정의
target_compile_definitions(breakout PRIVATE STB_IMAGE_IMPLEMENTATION)

# macOS에서 OpenGL 프레임워크 링크
if(APPLE)
    target_link_libraries(breakout "-framework OpenGL" "-framework Cocoa" "-framework IOKit" "-framework CoreVideo" glfw)
else()
    target_link_libraries(breakout OpenGL::GL glfw)
endif()

# C++ 표준 설정
target_compile_features(breakout PRIVATE cxx_std_17)
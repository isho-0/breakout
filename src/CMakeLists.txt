# 소스 파일
set(SOURCES
        main.cc

)

# 헤더 파일
set(HEADERS


)

# 실행 파일
add_executable(breakout ${SOURCES} ${HEADERS})

# 헤더 파일 경로 설정
target_include_directories(breakout PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

# C++ 표준 설정
target_compile_features(breakout PRIVATE cxx_std_17)
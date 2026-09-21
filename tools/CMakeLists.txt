# dependencies

find_package(Threads REQUIRED)

# third-party

# ...

# flags

llama_add_compile_flags()

# tools

if (EMSCRIPTEN)
else()
    # CachyLLama server-focused build: only build tools needed by the server
    # and diagnostic/benchmarking tooling. Shedded tools (completion,
    # perplexity, parser, gguf-split, fit-params, results,
    # cvector-generator, export-lora) are omitted for a leaner build.
    # batched-bench is included for benchmark.sh's batched test suite.
    add_subdirectory(cli)
    add_subdirectory(imatrix)
    add_subdirectory(batched-bench)
    add_subdirectory(llama-bench)
    add_subdirectory(quantize)
    if (LLAMA_BUILD_SERVER)
        if (LLAMA_BUILD_UI)
            add_subdirectory(ui)
        endif()
        add_subdirectory(server)
    endif()
    add_subdirectory(tokenize)
    add_subdirectory(tts)
    add_subdirectory(mtmd)
    if (GGML_RPC)
        add_subdirectory(rpc)
    endif()
endif()

# Add sources for the libOPENCALPHAD shared library
set(LIBOPENCALPHAD_SOURCES
    ${OCISOCBINDING_DIR}/liboctq.F90
    ${OCISOCBINDING_DIR}/liboctqisoc.F90
)

# Create the libOPENCALPHAD shared library
add_library(OPENCALPHAD SHARED ${LIBOPENCALPHAD_SOURCES})
target_link_libraries(OPENCALPHAD oc_essentials ${LAPACK_LIBRARIES} ${OPENMP_Fortran_LIBRARIES})

target_include_directories(OPENCALPHAD
    PUBLIC
        $<INSTALL_INTERFACE:include>
        $<BUILD_INTERFACE:${OCISOCBINDING_DIR}>
        ${OCISOCBINDING_DIR}
)

install(TARGETS OPENCALPHAD ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR})
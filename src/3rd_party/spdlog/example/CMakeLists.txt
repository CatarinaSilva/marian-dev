# *************************************************************************/
# * Copyright (c) 2015 Ruslan Baratov.                                    */
# *                                                                       */
# * Permission is hereby granted, free of charge, to any person obtaining */
# * a copy of this software and associated documentation files (the       */
# * "Software"), to deal in the Software without restriction, including   */
# * without limitation the rights to use, copy, modify, merge, publish,   */
# * distribute, sublicense, and/or sell copies of the Software, and to    */
# * permit persons to whom the Software is furnished to do so, subject to */
# * the following conditions:                                             */
# *                                                                       */
# * The above copyright notice and this permission notice shall be        */
# * included in all copies or substantial portions of the Software.       */
# *                                                                       */
# * THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,       */
# * EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF    */
# * MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.*/
# * IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY  */
# * CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,  */
# * TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE     */
# * SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.                */
# *************************************************************************/

cmake_minimum_required(VERSION 3.0)
project(SpdlogExamples)

if(TARGET spdlog)
  # Part of the main project
  add_library(spdlog::spdlog ALIAS spdlog)
else()
  # Stand-alone build
  find_package(spdlog CONFIG REQUIRED)
endif()

find_package(Threads)

add_executable(example example.cpp)
target_link_libraries(example spdlog::spdlog ${CMAKE_THREAD_LIBS_INIT})

add_executable(benchmark bench.cpp)
target_link_libraries(benchmark spdlog::spdlog ${CMAKE_THREAD_LIBS_INIT})

add_executable(multisink multisink.cpp)
target_link_libraries(multisink spdlog::spdlog ${CMAKE_THREAD_LIBS_INIT})

enable_testing()
file(MAKE_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/logs")
add_test(NAME RunExample COMMAND example)
add_test(NAME RunBenchmark COMMAND benchmark)

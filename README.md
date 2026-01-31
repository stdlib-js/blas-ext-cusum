<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# cusum

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Compute the cumulative sum along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.



<section class="usage">

## Usage

```javascript
import cusum from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-cusum@deno/mod.js';
```
The previous example will load the latest bundled code from the deno branch. Alternatively, you may load a specific version by loading the file from one of the [tagged bundles](https://github.com/stdlib-js/blas-ext-cusum/tags). For example,

```javascript
import cusum from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-cusum@v0.1.0-deno/mod.js';
```

You can also import the following named exports from the package:

```javascript
import { assign } from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-cusum@deno/mod.js';
```

#### cusum( x\[, initial]\[, options] )

Computes the cumulative sum along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0 ] );

var y = cusum( x );
// returns <ndarray>

var arr = ndarray2array( y );
// returns [ -1.0, 1.0, -2.0 ]
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a numeric or "generic" [data type][@stdlib/ndarray/dtypes].
-   **initial**: initial value for the cumulative sum (_optional_). May be either a scalar value or an [ndarray][@stdlib/ndarray/ctor] having a [data type][@stdlib/ndarray/dtypes] which [promotes][@stdlib/ndarray/promotion-rules] to the data type of the input [ndarray][@stdlib/ndarray/ctor]. If provided a scalar value, the value is cast to the data type of the input [ndarray][@stdlib/ndarray/ctor]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, an [ndarray][@stdlib/ndarray/ctor] initial value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor], an [ndarray][@stdlib/ndarray/ctor] initial value must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor]. By default, the initial value is the additive identity (i.e., zero).
-   **options**: function options (_optional_).

The function accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].
-   **dtype**: output ndarray [data type][@stdlib/ndarray/dtypes]. Must be a numeric or "generic" [data type][@stdlib/ndarray/dtypes].

By default, the function uses the additive identity when computing the cumulative sum. To begin summing from a different value, provide an `initial` argument.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0 ] );

var y = cusum( x, 10.0 );
// returns <ndarray>

var arr = ndarray2array( y );
// returns [ 9.0, 11.0, 8.0 ]
```

By default, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor]. To perform the operation over specific dimensions, provide a `dims` option.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0, 4.0 ], {
    'shape': [ 2, 2 ],
    'order': 'row-major'
});

var v = ndarray2array( x );
// returns [ [ -1.0, 2.0 ], [ -3.0, 4.0 ] ]

var y = cusum( x, {
    'dims': [ 0 ]
});
// returns <ndarray>

v = ndarray2array( y );
// returns [ [ -1.0, 2.0 ], [ -4.0, 6.0 ] ]

y = cusum( x, {
    'dims': [ 1 ]
});
// returns <ndarray>

v = ndarray2array( y );
// returns [ [ -1.0, 1.0 ], [ -3.0, 1.0 ] ]

y = cusum( x, {
    'dims': [ 0, 1 ]
});
// returns <ndarray>

v = ndarray2array( y );
// returns [ [ -1.0, 1.0 ], [ -2.0, 2.0 ] ]
```

By default, the function returns an [ndarray][@stdlib/ndarray/ctor] having a [data type][@stdlib/ndarray/dtypes] determined by the function's output data type [policy][@stdlib/ndarray/output-dtype-policies]. To override the default behavior, set the `dtype` option.

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import dtype from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-dtype@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0 ], {
    'dtype': 'generic'
});

var y = cusum( x, {
    'dtype': 'float64'
});
// returns <ndarray>

var dt = dtype( y );
// returns 'float64'
```

#### cusum.assign( x\[, initial], out\[, options] )

Computes the cumulative sum along one or more [ndarray][@stdlib/ndarray/ctor] dimensions and assigns results to a provided output [ndarray][@stdlib/ndarray/ctor].

```javascript
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-array@deno/mod.js';
import zerosLike from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-zeros-like@deno/mod.js';

var x = array( [ -1.0, 2.0, -3.0 ] );
var y = zerosLike( x );

var out = cusum.assign( x, y );
// returns <ndarray>

var v = ndarray2array( out );
// returns [ -1.0, 1.0, -2.0 ]

var bool = ( out === y );
// returns true
```

The method has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor]. Must have a numeric or generic [data type][@stdlib/ndarray/dtypes].
-   **initial**: initial value for the cumulative sum (_optional_). May be either a scalar value or an [ndarray][@stdlib/ndarray/ctor] having a [data type][@stdlib/ndarray/dtypes] which [promotes][@stdlib/ndarray/promotion-rules] to the data type of the input [ndarray][@stdlib/ndarray/ctor]. If provided a scalar value, the value is cast to the data type of the input [ndarray][@stdlib/ndarray/ctor]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, an [ndarray][@stdlib/ndarray/ctor] initial value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor], an [ndarray][@stdlib/ndarray/ctor] initial value must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor]. By default, the initial value is the additive identity (i.e., zero).
-   **out**: output [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The method accepts the following options:

-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   Both functions iterate over [ndarray][@stdlib/ndarray/ctor] elements according to the memory layout of the input [ndarray][@stdlib/ndarray/ctor]. Accordingly, performance degradation is possible when operating over multiple dimensions of a large non-contiguous multi-dimensional input [ndarray][@stdlib/ndarray/ctor]. In such scenarios, one may want to copy an input [ndarray][@stdlib/ndarray/ctor] to contiguous memory before computing the cumulative sum.
-   The output data type [policy][@stdlib/ndarray/output-dtype-policies] only applies to the main function and specifies that, by default, in order to avoid issues arising from integer overflow, the function must return an [ndarray][@stdlib/ndarray/ctor] having a [data type][@stdlib/ndarray/dtypes] amenable to accumulation. This means that, for integer data types having small value ranges (e.g., `int8`, `uint8`, etc), the main function returns an [ndarray][@stdlib/ndarray/ctor] having at least a 32-bit integer data type. By default, if an input [ndarray][@stdlib/ndarray/ctor] has a floating-point data type, the main function returns an [ndarray][@stdlib/ndarray/ctor] having the same data type. For the `assign` method, the output [ndarray][@stdlib/ndarray/ctor] is allowed to have any supported output [data type][@stdlib/ndarray/dtypes].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
import discreteUniform from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-array-discrete-uniform@deno/mod.js';
import getDType from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-dtype@deno/mod.js';
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import ndarray from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-ctor@deno/mod.js';
import cusum from 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-cusum@deno/mod.js';

// Generate an array of random numbers:
var xbuf = discreteUniform( 25, 0, 20, {
    'dtype': 'generic'
});

// Wrap in an ndarray:
var x = new ndarray( 'generic', xbuf, [ 5, 5 ], [ 5, 1 ], 0, 'row-major' );
console.log( ndarray2array( x ) );

// Perform operation:
var y = cusum( x, 100.0, {
    'dims': [ 0 ]
});

// Resolve the output array data type:
var dt = getDType( y );
console.log( dt );

// Print the results:
console.log( ndarray2array( y ) );
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-ext-cusum.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-ext-cusum

[test-image]: https://github.com/stdlib-js/blas-ext-cusum/actions/workflows/test.yml/badge.svg?branch=v0.1.0
[test-url]: https://github.com/stdlib-js/blas-ext-cusum/actions/workflows/test.yml?query=branch:v0.1.0

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-ext-cusum/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-ext-cusum?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-ext-cusum.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-ext-cusum/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-ext-cusum/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-ext-cusum/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-ext-cusum/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-ext-cusum/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-ext-cusum/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-ext-cusum/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-ext-cusum/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-ext-cusum/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/deno

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes/tree/deno

[@stdlib/ndarray/promotion-rules]: https://github.com/stdlib-js/ndarray-promotion-rules/tree/deno

[@stdlib/ndarray/output-dtype-policies]: https://github.com/stdlib-js/ndarray-output-dtype-policies/tree/deno

[@stdlib/ndarray/base/broadcast-shapes]: https://github.com/stdlib-js/ndarray-base-broadcast-shapes/tree/deno

</section>

<!-- /.links -->

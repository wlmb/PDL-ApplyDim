# NAME

PDL::ApplyDim - shuffle before and after applying function

# SYNOPSIS

    use PDL;
    use PDL::ApplyDim;
    my $nd=sequence(3,3);
    sub mult_columns($x, $dx, $m) { # multiply some columns of $x by $m
        $x->slice("0:-1:$dx")*=$m;
    }
    say $nd->apply_to(\&mult_columns, 1, 2, 3); #multiply even rows of $nd by 3
    say $nd->apply_not_to(\&mult_columns,0,2,3);# same

# DESCRIPTION

Many operations in PDL act on the first dimension, so a very common
idiom is

    $pdl->mv($dim,0)->function($some, $extra, $args)->mv(0, $dim);

to move the dimension `$dim` to the front, operate with the
function and the move the dimension back to its original place.
The idea is to hide the `mv` operations and write this as

    $pdl->apply_to(\&function, $dim, $some, $extra, $args);

or

    apply_to($pdl, "function", $dim, $some, $extra, $args);

Similarly

    $pdl->apply_not_to(\&function, $dim, $some, $extra, $args);

moves the dimension to the back.

Besides a number, `$dim` may also be an array reference, such as as
&#x3d;`[$d0, $d1...]`, to move the dimensions `$d0, $d1...` to the
front or to the back instead of just a single dimension.

# METHODS

## apply\_to($code, $dim, @extra\_args)

Applies `$code` to an ndarray after moving dimension `$dim` to the
front, and then bringing the dimension back to its original position.
Code can be a string naming a PDL function or a reference to a subroutine that acts on an
ndarray. It may take extra arguments. If &lt;$dim> is an array reference, moves
several dimensions.

## apply\_not\_to($code, $dim, @extra\_args)

Applies &lt;$code> to an ndarray after moving dimension `$dim` to the
end, and then bringing the dimension back to its original position.
Code can be a string naming a PDL function or a reference to a subroutine that acts on an
ndarray. It may take extra arguments. If &lt;$dim> is an array reference, moves
several dimensions.

# AUTHOR

W. Luis Mochan <mochan@fis.unam.mx>

# COPYRIGHT

Copyright 2025- W. Luis Mochan

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

\# =head1 SEE ALSO

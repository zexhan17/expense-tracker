<script>
    export let total;
    var ones = [
        "",
        "one",
        "two",
        "three",
        "four",
        "five",
        "six",
        "seven",
        "eight",
        "nine",
    ];
    var tens = [
        "",
        "",
        "twenty",
        "thirty",
        "forty",
        "fifty",
        "sixty",
        "seventy",
        "eighty",
        "ninety",
    ];
    var teens = [
        "ten",
        "eleven",
        "twelve",
        "thirteen",
        "fourteen",
        "fifteen",
        "sixteen",
        "seventeen",
        "eighteen",
        "nineteen",
    ];

    function convert_millions(num) {
        if (num >= 1000000) {
            return (
                convert_millions(Math.floor(num / 1000000)) +
                " million " +
                convert_thousands(num % 1000000)
            );
        } else {
            return convert_thousands(num);
        }
    }

    function convert_thousands(num) {
        if (num >= 1000) {
            return (
                convert_hundreds(Math.floor(num / 1000)) +
                " thousand " +
                convert_hundreds(num % 1000)
            );
        } else {
            return convert_hundreds(num);
        }
    }

    function convert_hundreds(num) {
        if (num > 99) {
            return (
                ones[Math.floor(num / 100)] +
                " hundred " +
                convert_tens(num % 100)
            );
        } else {
            return convert_tens(num);
        }
    }

    function convert_tens(num) {
        if (num < 10) return ones[num];
        else if (num >= 10 && num < 20) return teens[num - 10];
        else {
            return tens[Math.floor(num / 10)] + " " + ones[num % 10];
        }
    }

    function convert(num) {
        if (num == 0) return "zero";
        else return convert_millions(num);
    }
</script>

<div class="dropdown dropdown-top dropdown-left">
    <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
    <!-- svelte-ignore a11y-label-has-associated-control -->
    <label tabindex="0" class="hover:cursor-pointer {total ? 'underline' : ''}">
        {total}
    </label>
    <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
    <div
        tabindex="0"
        class="card compact dropdown-content z-[1] shadow bg-base-300 rounded-box w-64"
    >
        <div class="card-body">
            {convert(total)}
        </div>
    </div>
</div>

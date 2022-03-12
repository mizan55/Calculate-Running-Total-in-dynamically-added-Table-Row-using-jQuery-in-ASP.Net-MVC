public class HomeController : Controller
{
    // GET: /Home/
    public ActionResult Index()
    {
        return View();
    }
}
View

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
<div class="container">
    <div class="details">
        <table class="table table-responsive">
            <tr>
                <td>Rate</td>
                <td>Quantity</td>
                <td>Total</td>
                <td>&nbsp;</td>
            </tr>
            <tr class="mycontainer" id="mainrow">
                <td><input type="text" id="rate" class="rate form-control" onkeyup="CalculateTotal(this)" /></td>
                <td><input type="text" id="quantity" class="quantity form-control" onkeyup="CalculateTotal(this)" /></td>
                <td><input type="text" id="total" class="total form-control" /></td>
                <td><input type="button" id="add" value="Add" class="btn btn-success" /></td>
            </tr>
        </table>
        <hr />
        <div id="orderItems">
            <table class="table table-responsive" id="orderdetailsItems">
            </table>
            <span>Grand Total : <span id="lblGrandTotal"></span></span>
        </div>
    </div>
</div>
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css" />
<script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script type="text/javascript">
    $(document).ready(function () {
        //Add button click event
        $('#add').click(function () {
            var $newRow = $('#mainrow').clone().removeAttr('id');
            $('#quantity,#total,#rate,#add', $newRow).removeAttr('id');
            $('#orderdetailsItems').append($newRow);
            $('#quantity,#rate,#total').val('');
            CalculateGrandTotal();
        });
    });
    function CalculateTotal(ele) {
        var rate = $(ele).closest('tr').find('.rate').val();
        var quantity = $(ele).closest('tr').find('.quantity').val();
        rate = rate == '' ? 0 : rate;
        quantity = quantity == '' ? 0 : quantity;
        if (!isNaN(rate) && !isNaN(quantity)) {
            var total = parseFloat(rate) * parseFloat(quantity);
            $(ele).closest('tr').find('.total').val(total.toFixed(2));
        }
        CalculateGrandTotal();
    }
    function CalculateGrandTotal() {
        var grandTotal = 0;
        $.each($('#orderdetailsItems').find('.total'), function () {
            if ($(this).val() != '' && !isNaN($(this).val())) {
                grandTotal += parseFloat($(this).val());
            }
        });
        $('#lblGrandTotal').html(grandTotal.toFixed(2));
    }
</script>


Package containing functions to templates.

author: Marcos Thomaz da Silva 
        Email: marcosthomazs@gmail.com

======================================================
File/Module: summary.py
======================================================


-----------------------------------------------------
Class Cel()
-----------------------------------------------------
 - class Helper used to store summaries
 - Used internally in class VirtualSummary
 
 
-----------------------------------------------------
Class VirtualSummary()
-----------------------------------------------------
    Class to be instantiated in views and used within the templates.
    Usage (only in django templates):
        vs = VirtualSummary()
        
        {{ vs.<your_field_to_summary> }}  = Create a new virtual field to store the summary
        {{ vs.<your_field_to_summary>|add:<value_to_sum> }} = Use the fielter "add" 
                                                              to realize the sum.
        {{ vs.total__<your_field_to_summary> }} = returns the result of the sum
        {{ vs.reset__<your_field_to_summary> }} = reset the sum and 
                                                  return None. Used 
                                                  for realize summary 
                                                  in groups/subgroups
        
        
    ================================================
    Complete Example:
    ================================================
    
    class Sale(models.Model):
    
        product = models.ForeignKey(Product)
        quantity = models.IntegerField()
        value = models.DecimalField('Unitary Value', max_digits=7, decimal_places=2)
        
        @property
        def subtotal(self):
            return self.quantity * self.value
        
        def __unicode__(self):
            return self.product.name
    
    
    def myview(request):
        from django_template_plus.summary import VirtualSummary
        vtable = VirtualSummary()
        my_sales = Sale.objects.all()
        return render(request, 'your_template.html' , locals())
        
    
    ======= your_template.html =====
    <html>
        <body>
            <table>
                <thead>
                    <tr>
                        <th>Product</th>
                        <th>Quantity</th><!-- {{ vtable.qty }} -->
                        <th>Un.Value</th><!-- {{ vtable.unval }} -->
                        <th>Subtotal</th><!-- {{ vtable.subtot }} -->
                    </tr>
                </thead>
                <tbody>
                    {% for sale in my_sales %}
                    <tr>
                        <td>{{ sale.product }}</td>
                        <td>{{ vtable.qty|add:sale.quantity }}</td>
                        <td>{{ vtable.unval|add:sale.value }}</td>
                        <td>{{ vtable.subtot|add:sale.subtotal }}</td>
                    </tr>
                    {% endfor %}
                </tbody>
                <tfooter>
                    <tr>
                        <th>Total</th>
                        <th>{{ vtable.total__qty }}</th>                        
                        <th>{{ vtable.total__unval }}</th>                        
                        <th>{{ vtable.total__subtot }}</th>                        
                    </tr>
                </tfooter>
            </table>
        </body>
    </html>

    
TODO:
----------------------------------------
Another operations: Subtraction, Average and Median


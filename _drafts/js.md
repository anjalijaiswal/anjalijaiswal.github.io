
  handleSubmit: (event) ->
    handleAFClick event
    checked_data = $('#leave_type_radio :checkbox:checked')
    leave_types_arry = []
    i = 0
    emps = SaralDataTables.getAllSelectedRows('#leave_report_table');
    while i < checked_data.length
      leave_types_arry.push checked_data[i].value
      i++
    $el = $('<input />',
      'id': 'leave_types_id'
      'name': 'leave_types[]'
      'value': leave_types_arry
      'type': 'hidden')
    $el2 = $('<input />',
      'id': 'selected_employees_id'
      'name': 'selected_employees[]'
      'value': emps
      'type': 'hidden')
    leaveTypeExists = document.getElementById("leave_types_id");
    selectedEmployeesExists = document.getElementById("selected_employees_id");

    if(leaveTypeExists)
      $('#leave_types_id').val(leave_types_arry)
    else
      $('#leave_report').append $el

    if(selectedEmployeesExists)
      $('#selected_employees_id').val(emps)
    else
      $('#leave_report').append $el2
    return

  checkFieldsValid: ->
    paymonths = []
    error = []
    $('.report_error_message').empty()
    $.ajax
      url: '/leave_reports/fetch_paymonths'
      type: 'GET'
      dataType: 'json'
      success: (json_obj) ->
        $.each json_obj, (index, value) ->
          paymonths.push(value.month_name)
          return
        if paymonths.includes($('#from_date').val())
          error.push('Please select valid from month')
        if paymonths.includes($('#to_date').val())
          error.push('Please select valid to month')
        if paymonths.includes($('#paymonth').val())
          error.push('Please select valid paymonth')
        console.log(paymonths)
      fail: (data) ->
        error = $('<div>"Some Error occured. Please try again "</div>')
        $('.report_error_message').append("<div class='alert alert-danger'>" + error + "</div>")
        return
    if $('#leave_type_radio :checkbox:checked').length < 1
      error.push('Please select atleast one Leave Type')
    if error.length > 0
      $('.report_error_message').append("<div class='alert alert-danger'></div>")
      $('.report_error_message')
      git
      return false
    else
      return true

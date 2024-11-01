$(document).ready(function() {
    // Form Elements
    const suiteNumberInput = $('#suite-number');
    const entryDateInput = $('#entry-date');
    const securityCheckbox = $('#security');
    const securityOptions = $('#security-options');
    const guardNameSelect = $('#guard-name');
    const otherGuardNameInput = $('#other-guard-name');
    const otherPersonnelCheckbox = $('#other-personnel');
    const otherPersonnelNameInput = $('#other-personnel-name');
    const entryTypeSelect = $('#entry-type');
    const natureOfVisitInput = $('#nature-of-visit');
    const optionsCheckboxes = $('.form-check-input');
    const noticesPerPageSelect = $('#notices-per-page');
    const printButton = $('#print-button');
    const noticePreviewContainer = $('#notice-preview-container');
    const printableArea = $('#printable-area');

    // Dynamic Form Behavior
    securityCheckbox.change(function() {
        if ($(this).is(':checked')) {
            securityOptions.removeClass('d-none');
        } else {
            securityOptions.addClass('d-none');
            guardNameSelect.val('');
            otherGuardNameInput.val('').addClass('d-none');
        }
        updateNotice();
    });

    guardNameSelect.change(function() {
        if ($(this).val() === 'Others') {
            otherGuardNameInput.removeClass('d-none');
        } else {
            otherGuardNameInput.val('').addClass('d-none');
        }
        updateNotice();
    });

    otherPersonnelCheckbox.change(function() {
        if ($(this).is(':checked')) {
            otherPersonnelNameInput.removeClass('d-none');
        } else {
            otherPersonnelNameInput.val('').addClass('d-none');
        }
        updateNotice();
    });

    // Update Notice Preview
    $('#notice-form input, #notice-form select, #notice-form textarea').on('input change', function() {
        updateNotice();
    });

    function updateNotice() {
        const noticeData = collectNoticeData();
        const noticesPerPage = parseInt(noticesPerPageSelect.val());
        noticePreviewContainer.html('');
        for (let i = 0; i < noticesPerPage; i++) {
            const noticeHTML = generateNoticeHTML(noticeData);
            noticePreviewContainer.append(`
                <div class="notice">
                    ${noticeHTML}
                </div>
            `);
        }
    }

    function collectNoticeData() {
        const suiteNumber = suiteNumberInput.val() || '____________';
        const entryDate = entryDateInput.val() ? formatDate(entryDateInput.val()) : '____________';
        let personsWhoEntered = [];
        $('#notice-form .form-check-input[type="checkbox"]:checked').each(function() {
            const value = $(this).val();
            if (value === 'Security') {
                let guardName = guardNameSelect.val();
                if (guardName === 'Others') {
                    guardName = otherGuardNameInput.val() || '____________';
                }
                if (guardName) {
                    personsWhoEntered.push(`Security (${guardName})`);
                } else {
                    personsWhoEntered.push('Security');
                }
            } else if (value === 'Other') {
                const otherName = otherPersonnelNameInput.val() || '____________';
                personsWhoEntered.push(otherName);
            } else if (value !== 'Work Completed' && value !== 'Work Pending' && value !== 'Please Contact Property Management') {
                personsWhoEntered.push(value);
            }
        });
        if (personsWhoEntered.length === 0) {
            personsWhoEntered.push('____________');
        }

        const entryType = entryTypeSelect.val() || '____________';
        const natureOfVisit = natureOfVisitInput.val() || '____________';

        let options = [];
        $('#notice-form .form-check-input[type="checkbox"]').each(function() {
            const value = $(this).val();
            if (value === 'Work Completed' || value === 'Work Pending' || value === 'Please Contact Property Management') {
                options.push({
                    label: value,
                    checked: $(this).is(':checked')
                });
            }
        });

        return {
            suiteNumber,
            entryDate,
            personsWhoEntered: personsWhoEntered.join(', '),
            entryType,
            natureOfVisit,
            options
        };
    }

    function generateNoticeHTML(data) {
        let optionsHTML = '';
        data.options.forEach(function(option) {
            const symbol = option.checked ? '☑' : '☐';
            optionsHTML += `<div><span>${symbol}</span><span>${option.label}</span></div>`;
        });

        return `
            <img src="https://i.imgur.com/LmweghF.png" alt="Company Logo" class="logo">
            <h2>SUITE ENTRY NOTICE</h2>
            <img src="https://i.imgur.com/7O6EOHU.png" alt="Lock Image" class="lock">
            <p><strong>Date:</strong> ${data.entryDate}</p>
            <p><strong>Suite Number:</strong> ${data.suiteNumber}</p>
            <p><strong>Person(s) who entered:</strong> ${data.personsWhoEntered}</p>
            <p><strong>Entry Type:</strong> ${data.entryType}</p>
            <p><strong>Nature of Visit:</strong></p>
            <p>${data.natureOfVisit}</p>
            <div class="options">
                ${optionsHTML}
            </div>
            <p class="footer">Questions? Contact Property Management: 647-368-7395</p>
        `;
    }

    function formatDate(dateString) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' };
        const date = new Date(dateString);
        return date.toLocaleDateString(undefined, options);
    }

    // Initial Notice Update
    updateNotice();

    // Print Functionality
    printButton.click(function() {
        printableArea.html('');
        const noticeData = collectNoticeData();
        const noticesPerPage = parseInt(noticesPerPageSelect.val());

        for (let i = 0; i < noticesPerPage; i++) {
            const noticeHTML = generateNoticeHTML(noticeData);
            printableArea.append(`
                <div class="notice">
                    ${noticeHTML}
                </div>
            `);
        }

        window.print();
    });

    // Update notice preview when notices per page changes
    noticesPerPageSelect.change(function() {
        updateNotice();
    });
});
